# Flutter App Security Checklist

Ensuring the security of your Flutter app is crucial to protect user data, prevent unauthorized access, and maintain the integrity of your app. Below is a comprehensive list of security measures every Flutter developer should take.

---

## 1. **Secure Storage of Sensitive Data**

* Use `flutter_secure_storage` to store sensitive data (tokens, passwords).
* Avoid using `SharedPreferences` for any sensitive information.

## 2. **Use HTTPS for All Network Calls**

* Always use `https` over `http` to encrypt data in transit.
* Add HTTPS pinning if needed using packages like `http` or `dio` with custom security context.

## 3. **Validate All Inputs**

* Sanitize user input to avoid injection attacks.
* Use form validators and regular expressions to restrict input formats.

## 4. **Avoid Hardcoded Secrets**

* Do not store API keys or secrets directly in your Dart code.
* Use environment variables or secure backend storage.
* For Android, use the NDK or Keystore. For iOS, use Keychain.

## 5. **Obfuscate and Minify Code**

* Use Dart’s `--obfuscate` flag during build:

```sh
flutter build apk --obfuscate --split-debug-info=/<project-name>/debug-info
```

* This makes reverse engineering harder.

## 6. **Restrict Permissions**

* Only request necessary permissions (location, camera, storage, etc.).
* Regularly review permissions in `AndroidManifest.xml` and `Info.plist`.

## 7. **Implement Authentication and Authorization**

* Use secure authentication methods (OAuth2, Firebase Auth).
* Validate tokens on the server side.
* Implement role-based access control (RBAC).

## 8. **Secure APIs and Backend**

* Use proper authentication and authorization on APIs.
* Implement rate limiting and throttling.
* Use firewalls and API gateways.

## 9. **Enable Certificate Pinning**

* Prevent man-in-the-middle attacks by pinning certificates.
* Use packages like `http` + custom `SecurityContext` or `dio` interceptors.

## 10. **Detect and Prevent Jailbreak/Root Access**

* Use packages like `root_checker`, `jailbreak_detection` to detect compromised devices.
* Restrict app functionality if root/jailbreak is detected.

## 11. **Handle Errors Securely**

* Do not expose internal logs or stack traces to users.
* Log errors securely using crash reporting tools (Firebase Crashlytics, Sentry).

## 12. **Use Biometrics or Device Authentication**

* Use `local_auth` package for fingerprint, face ID, etc.
* Add an additional layer of security for sensitive actions.

## 13. **Secure WebViews**

* Use `flutter_inappwebview` or similar with security options enabled.
* Disable JavaScript unless necessary.
* Prevent navigation to unknown URLs.

## 14. **Use Security Headers for Web Apps**

* Set CSP (Content Security Policy), XSS protection, etc., for Flutter Web.

## 15. **Code Reviews and Security Audits**

* Regularly review code for security flaws.
* Use static code analyzers and linters.

## 16. **Use Strong Encryption Algorithms**

* Always encrypt data at rest and in transit.
* Use AES or RSA for encryption needs.

## 17. **Prevent Screen Recording and Screenshots (Optional)**

* Android:

```dart
SystemChrome.setEnabledSystemUIMode(SystemUiMode.manual, overlays: []);
```

* iOS: Use `isSecureTextEntry = true` for sensitive fields.

---

## Final Tips

* Stay updated with latest Flutter and dependency security patches.
* Educate your team, especially juniors, about common security pitfalls.
* Test your app with tools like OWASP ZAP or Mobile Security Framework (MobSF).

---

## Resources

* [OWASP Mobile Security](https://owasp.org/www-project-mobile-top-10/)
* [Flutter Secure Storage](https://pub.dev/packages/flutter_secure_storage)
* [Flutter Obfuscation Guide](https://docs.flutter.dev/deployment/obfuscate)
* [Dart Security Best Practices](https://dart.dev/guides/libraries/security)

Securing your Flutter app is an ongoing effort, not a one-time task. Building a secure app from day one saves time, builds trust, and keeps your users safe.