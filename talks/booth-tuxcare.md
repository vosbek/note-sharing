---
title: "TuxCare: rebuilt, patched open-source packages, including for end-of-life Spring and Angular"
---

# TuxCare: rebuilt, patched open-source packages, including for end-of-life Spring and Angular

Booth visit: TuxCare · QCon SF 2026 · Wed Nov 18

> TuxCare supplies open-source packages rebuilt from source and keeps patching them after upstream support ends, served from a repository that a repository manager such as Artifactory or Nexus can proxy.

## Key points

- SecureChain serves Python, PHP, Rust, Java, npm and Go packages rebuilt from source and scanned for malware, each with an SBOM, VEX data and SLSA Level 3 provenance.
- You point a repository manager such as JFrog Artifactory, Sonatype Nexus or GitHub Packages at it, and their Java page says Maven and Gradle builds keep working unchanged.
- Endless Lifecycle Support keeps shipping CVE fixes after upstream support ends; the list includes Spring, Hibernate, Struts, AngularJS 1.5 to 1.8 and Angular 4 to 19.
- The pages promise patches under an SLA but give no response times, and no prices; SLSA Level 3 for the end-of-life packages is listed as coming soon.
- TuxCare has no AI product; its homepage argues AI is making open-source packages faster to attack and exploit.

Booth, Wednesday Nov 18. Sources: TuxCare's homepage, SecureChain for Java page and Endless Lifecycle Support for language ecosystems page, read Nov 18, 2026. Figures and claims are the vendor's own until we test them.

## What it is

TuxCare sells open-source supply chain security across the life of a package: verified builds while a project is maintained, then security patches after upstream support ends. It covers operating systems and Linux kernels as well as language libraries and frameworks.

## How it works

- **SecureChain.** Packages rebuilt from source in isolated environments, screened for malware and suspicious code, and shipped with an SBOM, VEX data and SLSA Level 3 provenance. A missing package is added on request at no extra cost, they say.
- **Delivery.** A repository you point Artifactory, Nexus or GitHub Packages at, or point a package manager at directly.
- **Endless Lifecycle Support.** Signed, tested binary patches published to TuxCare-hosted repositories after a framework or runtime reaches end of life, so builds pick them up like any other update.
- **Rebootless patching.** KernelCare patches Linux kernels and LibCare patches OpenSSL and glibc without a reboot.

## Where it connects to the talks

No talk covered package supply chain directly. The link is to modernization. A framework upgrade is the kind of large, mechanical change teams now hand to coding agents, and TuxCare is what you pay for instead of doing it.

## Docs and getting started

- [Supported language ecosystems](https://tuxcare.com/endless-lifecycle-support/language-ecosystems/)
- [Spring end-of-life support](https://tuxcare.com/endless-lifecycle-support/java-spring-eol-support/)
- [AngularJS end-of-life support](https://tuxcare.com/endless-lifecycle-support/angularjs-eol-support/)
- [ELS for libraries docs](https://docs.tuxcare.com/els-for-libraries/)
- [SecureChain for Java](https://tuxcare.com/securechain-for-oss/java/)
