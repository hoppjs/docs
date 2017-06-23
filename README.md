<p align="center">
  <img src="img/logo.png">
</p>
<p align="center">Crazy rapid build system.</p>

<p align="center">
  <a href="https://travis-ci.org/hoppjs/hopp"><img alt="Travis CI" src="https://travis-ci.org/hoppjs/hopp.svg?branch=master"></a>
  <img alt="node v4 to 8" src="https://img.shields.io/badge/node-v4%20to%208-brightgreen.svg?style=flat">
</p>

## Welcome to hopp

It's a crazy rapid build system. The concepts behind hopp that make it
fast are hidden away in this documentation. We've targeted this documentation
at users who want to **use hopp**, hackers that want to **learn about hopp**, and
developers who want to **build for hopp**.

To navigate through the documentation, use the sidebar.

## Why hopp?

 1. **Ridiculously fast.** It was the reason we originally built hopp.
 We realized how much time was being wasted waiting for builds to finish.
 We also realized that all build tools claim to be the fastest. So we first
 developed benchmarks to verify the performance of build tools under various
 conditions over at [buildjs-benchmarks](https://travis-ci.org/hoppjs/buildjs-benchmarks).
 We use these benchmarks to continuously test the performance of hopp as we
 add and remove features.
 2. **Super magical.** This is an opinion-based issue but many developers
 shy away from automation and say it is too *magical*. hopp does things a bit
 differently. We try to wave magic wands and say abracadabra whenever possible.
 Like autoloading plugins & managing bundling.
 3. **Built to scale.** Though the performance issues of other build tools is
 a bit painful, it really affects the build process of really large projects.
 hopp was built to perform well not just for smaller projects but also for large
 projects that their tools to perform at scale.

## License

Copyright &copy; 2017 10244872 Canada Inc.

All code & docs are licensed under the [MIT](LICENSE.md) license.