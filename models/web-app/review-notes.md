# Web Application: Review Notes

An honest review of this reference model: what it covers well and where it falls short. Use it as a checklist when adapting the model to your own system. Back to the [model overview](README.md).

## The following threats are missing here

1- Injection Flaws from browser

2. Cross-Site Scripting (XSS), which is the #1 way attackers steal session tokens in web apps.

3: Cross-Site Request Forgery (CSRF), which is addressed in several frameworks, but if the framework is not specified, it should be mentioned as a classic threat.

4. Cryptographic Failures (Data in Transit/Rest). Because data flows have no attributes it is not clear if this threat is present so I think in a general web application threat model, the threat for Weak Encryption should be considered.

5: Clickjacking / UI Redressing where attackers can load your website inside a transparent &lt;iframe> and trick users into clicking buttons they didn't intend to.
