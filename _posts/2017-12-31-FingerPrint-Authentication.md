---
title:  "FingerPrint Authentication"
date:   2017-06-12
author: Ashutosh Singh
categories:
- blog
tags:
- android
---

Android Fingerprint authentication uses smartphone touch sensor to authenticate the user. Android Marshmallow has introduced a set of API that makes it easy to use the touch sensor. Before Android Marshmallow, the method to access the touch sensor was not standard.

### The benefit of Fingerprint Authentication

* Fast and easy to use
* Secure: fingerprint uniquely identifies you
* Online transactions are safer


### implemention of FingerPrint Authentication

To authenticate users via the fingerprint scan, get an instance of the new FingerprintManager class and call the authenticate() method. Your app must be running on a compatible device with a fingerprint sensor.
Steps to enable `FingerPrint Authentication`

* Verify that the lock screen is secure, or in other words, it is protected by PIN, password or pattern.
* Verify that at least one fingerprint is registered on the smartphone
* Get access to Android keystore to store the key used to encrypt/decrypt an object.
* Generate an encryption key and the Cipher.
* Start the authentication process and implement a callback class to handle authentication events.


#### Enable the permission in manifest

```
<uses-permission android:name="android.permission.USE_FINGERPRINT" />
```

#### Check the device compatibility.

```
keyguardManager = (KeyguardManager) getSystemService(KEYGUARD_SERVICE);
fingerprintManager = (FingerprintManager) getSystemService(FINGERPRINT_SERVICE);

private boolean checkDeviceCompatibility() {
  if (Build.VERSION.SDK_INT < Build.VERSION_CODES.M) return false;

       // Check whether the device has a Fingerprint sensor.
  if (!fingerprintManager.isHardwareDetected()) {
      return false;
  }

  if (ActivityCompat.checkSelfPermission(this, Manifest.permission.USE_FINGERPRINT) != PackageManager.PERMISSION_GRANTED) {
     showMessage(stringFingerPrintPermissionError);
     return false;
  }

  if (!fingerprintManager.hasEnrolledFingerprints()) {
      showMessage(stringNoFingerPrintError);
      return false;
  }

  // Checks whether lock screen security is enabled or not
  if (!keyguardManager.isKeyguardSecure()) {
      showMessage(stringLockScreenNotEnable);
      return false;
  }

  return true;
}
```

#### Access to Android Keystore and Generate the Key

If the device is compatible, then generate the key.

```
@TargetApi(Build.VERSION_CODES.M)
    private void generateKey() {
        try {
            keyStore = KeyStore.getInstance("AndroidKeyStore");
        } catch (Exception e) {
            e.printStackTrace();
        }

        KeyGenerator keyGenerator;
        try {
            keyGenerator = KeyGenerator.getInstance(KeyProperties.KEY_ALGORITHM_AES, "AndroidKeyStore");
        } catch (NoSuchAlgorithmException | NoSuchProviderException e) {
            throw new RuntimeException("Failed to get KeyGenerator instance", e);
        }

        try {
            keyStore.load(null);
            keyGenerator.init(new KeyGenParameterSpec.Builder(KEY_NAME,
                    KeyProperties.PURPOSE_ENCRYPT | KeyProperties.PURPOSE_DECRYPT)
                    .setBlockModes(KeyProperties.BLOCK_MODE_CBC)
                    .setUserAuthenticationRequired(true)
                    .setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_PKCS7)
                    .build());
            keyGenerator.generateKey();
        } catch (NoSuchAlgorithmException | InvalidAlgorithmParameterException | CertificateException | IOException e) {
            throw new RuntimeException(e);
        }
    }
```

#### Create the Android Cipher

After generating the key, initialize the cipher that uses the key.

```
@TargetApi(Build.VERSION_CODES.M)
   public boolean cipherInit() {
       try {
           cipher = Cipher.getInstance(KeyProperties.KEY_ALGORITHM_AES + "/" + KeyProperties.BLOCK_MODE_CBC + "/" + KeyProperties.ENCRYPTION_PADDING_PKCS7);
       } catch (NoSuchAlgorithmException | NoSuchPaddingException e) {
           throw new RuntimeException("Failed to get Cipher", e);
       }

       try {
           Signature.getInstance("SHA256withECDSA");
           keyStore.load(null);
           SecretKey key = (SecretKey) keyStore.getKey(KEY_NAME, null);
           cipher.init(Cipher.ENCRYPT_MODE, key);
           return true;
       } catch (KeyPermanentlyInvalidatedException e) {
           return false;
       } catch (KeyStoreException | CertificateException | UnrecoverableKeyException | IOException | NoSuchAlgorithmException | InvalidKeyException e) {
           throw new RuntimeException("Failed to init Cipher", e);
       }
   }
```

#### If Cipher is initialized then we authenticate the finger print.

```
if (cipherInit()) {
            FingerprintManager.CryptoObject cryptoObject = new FingerprintManager.CryptoObject(cipher);
            FingerprintHandler helper = new FingerprintHandler(this);
            helper.startAuth(fingerprintManager, cryptoObject);
}
```

Create the callback class so that we can receive event notification and we can know when the authentication succeeded or something went wrong. This class extends FingerprintManager.AuthenticationCallback.

```
@TargetApi(Build.VERSION_CODES.M)
public class FingerprintHandler extends FingerprintManager.AuthenticationCallback {

    private Activity mActivity;

    public FingerprintHandler(Activity activity) {
        mActivity = activity;
    }

    public void startAuth(FingerprintManager manager, FingerprintManager.CryptoObject cryptoObject) {
        CancellationSignal cancellationSignal = new CancellationSignal();
        if (ActivityCompat.checkSelfPermission(mActivity, Manifest.permission.USE_FINGERPRINT) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        manager.authenticate(cryptoObject, cancellationSignal, 0, this, null);
    }

    @Override
    public void onAuthenticationError(int errMsgId, CharSequence errString) {
       // on authentication error.
    }

    @Override
    public void onAuthenticationHelp(int helpMsgId, CharSequence helpString) {

    }

    @Override
    public void onAuthenticationFailed() {
        // on authentication failure.
    }

    @Override
    public void onAuthenticationSucceeded(FingerprintManager.AuthenticationResult result) {
      // After succefull authentication.
    }
}
```

Now we have finished the `FingerPrint authentication`.
