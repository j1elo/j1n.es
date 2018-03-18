---
title: "Kurento 6.7 Release: Moving Forward"
date: 2018-03-18T00:59:05+01:00
draft: true

featuredImage: ""
author: "Juan"
categories: ["kurento"]
tags: []
---

It's been a while since Kurento was [acqui-hired by Twilio][1-1], more than one year ago. Since then, the project lost almost all of its momentum, and it entered a "minimal maintenance" mode. Understandably, [some people][1-2] were wondering whether the Kurento Media Server would end up becoming abandonware.

Fear not, work hasn't stopped behind the curtains. On the contrary: a new team has been formed, and lots of necessary infrastructure updates have been introduced. We know that the rhythm has been slow, but believe us when we say that we are ready to start rocking streaming again!

So let's talk about the new team behind Kurento, what is the current status of the project, the roadmap for the future, and a new complementary project started by this team: **[OpenVidu][1-3]**.

Last but not least, let us introduce a new official release, which marks the start of this new development cycle for the project: **Kurento 6.7**.

[1-1]: https://www.kurento.org/blog/whats-next-kurento-and-elasticrtc
[1-2]: https://bloggeek.me/whats-new-jitsi-videobridge/
[1-3]: http://openvidu.io/

<!--more-->

## Development team

The Kurento development team is formed under the [CodeURJC Research Group][2-1], which belongs to the spanish [Rey Juan Carlos University][2-2], located in Madrid. This team is financed by the University and by [Naeva Tec][2-3].

- **[Micael Gallego][2-4]** is the current lead of the Kurento project. He is involved mainly in the development of the [Kurento Java client][2-10], [Java tutorials][2-11], [testing infrastructure][2-12] and [Kurento Module Creator][2-13].

- **[Boni García][2-5]** is involved in [testing infrastructure][2-12] and also in writing tutorials and [documentation][2-14].

- **[Pablo Fuente][2-6]** works in [Kurento Room][2-15], [OpenVidu][2-16], [Kurento Java client][2-10] and the [JavaScript client][2-17] libraries.

- **[Juan Navarro][2-7]** is our [Kurento][2-18] [Media][2-19] [Server][2-20] guy. He loves working close to the metal with C/C++ and GStreamer.

- **[Fede Díaz][2-8]** is our DevOps, helping the project with [CI infrastructure][2-21], performance testing, and so on.

- **[Patxi Gortázar][2-9]** is the original DevOps of Kurento platform and he's still working across several areas of the project.

[2-1]: https://www.codeurjc.es/
[2-2]: https://www.urjc.es/
[2-3]: https://www.naevatec.com

[2-4]: https://github.com/micaelgallego
[2-5]: https://github.com/bonigarcia
[2-6]: https://github.com/pabloFuente
[2-7]: https://github.com/j1elo
[2-8]: https://github.com/nordri
[2-9]: https://github.com/gortazar

[2-10]: https://github.com/Kurento/kurento-java/tree/master/kurento-client
[2-11]: https://github.com/Kurento/kurento-tutorial-java
[2-12]: https://github.com/Kurento/kurento-java/tree/master/kurento-integration-tests
[2-13]: https://github.com/Kurento/kurento-module-creator
[2-14]: https://github.com/Kurento/doc-kurento
[2-15]: https://github.com/Kurento/kurento-room
[2-16]: http://openvidu.io/
[2-17]: https://github.com/Kurento/kurento-utils-js
[2-18]: https://github.com/Kurento/kms-core
[2-19]: https://github.com/Kurento/kms-elements
[2-20]: https://github.com/Kurento/kms-filters
[2-21]: https://github.com/Kurento/adm-scripts



## Introducing OpenVidu

While Kurento implements a powerful engine, able to manage a multitude of use cases and complex scenarios, we found that a lot of users were interested in the more basic and simpler idea (but still technically difficult to accomplish) of typical videoconference rooms.

With this in mind, we started working on a complementary solution that *builds upon Kurento*, to provide an easy to use and effective way of creating and managing videoconference rooms, adding video calls to web or mobile applications. OpenVidu acts as a wrapper around a standard installation of Kurento Media Server, and takes care of all the complexities inherent to WebRTC video calls such as SDP negotiation, ICE connectivity checks, video/audio codec compatibility, etc.

Also, a very important planned feature of OpenVidu will be to provide seamless scaling of Kurento resources over multiple servers, providing in one single and compact package what is currently being done manually by Kurento users in their own applications.

Check out the [OpenVidu][3-1] project page, which contains all the relevant information: http://openvidu.io/

Besides this, we have migrated some parts of our infrastructure to be hosted under the OpenVidu name (such as the Debian package repositories, which now are under the `openvidu.io` domain) and it is possible that more migrations happen over time.

[3-1]: http://openvidu.io/



## Kurento Status and Roadmap

We want Kurento to become the reference media server for streaming and WebRTC communications. The bulk of work done in the last year has been focused on rebuilding our Continuous Integration infrastructure, fixing bugs in Kurento Media Server, and adding some small features that had been asked for by some customers.

Our immediate next steps will be to redirect our attention back to the greater community: both the mailing list and the issue tracker are full of topics that require our consideration.

We don't have a strict roadmap with specific dates, but we do have a very clear idea of what are our intended next steps in terms of feature development for Kurento and OpenVidu:

Kurento Media Server:

- Support Safari browser (preliminary support already available in Kurento 6.7).
- Support Microsoft Edge browser.
- Update GStreamer and several other underlying support libraries to their latest versions.
- Review the documentation. Unify and merge all bits of information that have been scattered over time.
- Review all tutorials. Ensure that everything is working properly.
- Review and clean up all open issues in the bug tracker.

OpenVidu:

- Improve features and stability of videoconference recording.
- Enable peer-to-peer calls, without an intermediate media server.
- Add a moderator role.
- Start planning the intended auto-scaling capabilities.



## Kurento Media Server 6.7

This has been a busy year for the Kurento team, although sadly the results of it aren't very colorful to show off in a blog post. The latest release of Kurento is a minor point release, which means that some features have been added but this server is still backwards-compatible with previous client applications.



### Debian packages

There are some changes in the packaging of KMS: previously, all packages (as installed with `apt-get install`) included the suffix `-6.0` in their name (for example: *kms-core-6.0*). We have changed the way new KMS releases will be distributed, so now there is no need to have the explicit major version in the package names. Starting from version 6.7, all package names will consist of only the actual name, without any suffix. For example, *kurento-media-server-6.0* becomes *kurento-media-server*.

The ability to install old releases of KMS had been broken for a while, so we rebuilt the CI scripts from the ground up, to recover this feature. Starting with this release, each independent new release of KMS will be available to install in its own package repository, and users will be able to manually choose their preferred versions by changing the later part of the URL that is written in the file `/etc/apt/sources.list.d/kurento.list`:

    deb http://ubuntu.openvidu.io/6.7.0 xenial kms6



### New documentation

The whole documentation of Kurento has been fully reviewed, from back to front, in an attempt to unify all corrections and random annotations that we had noticed over the time but never got to edit into the actual text. Also, the structure of the documents has been reworked in an attempt to provide for a more natural reading flow.

Some highlights of the new documentation would be the [Getting Started][4-1] and [Installation][4-2] guides, and the new [Developer Guide][4-3], which until now had been sitting in a shared Google Docs document (not the best option for discoverability!).

Head to the documentation main page to see what is up with Kurento: https://doc-kurento.readthedocs.io/en/latest/

[4-1]: https://doc-kurento.readthedocs.io/en/latest/user/quickstart.html
[4-2]: https://doc-kurento.readthedocs.io/en/latest/user/installation.html
[4-3]: https://doc-kurento.readthedocs.io/en/latest/dev/development.html



### Safari preliminary support

We've integrated all required changes that were needed to make Kurento play nicely with Safari browsers. These changes are still considered to be in a preview state, while more exhaustive testing is taking place.

If you want to help with testing Safari in different Apple devices & Safari versions, we opened a thread in our Google Groups mailing list, where any user who wants to collaborate is able to do so: https://groups.google.com/forum/#!topic/kurento/rWZroM3SBWk



### RTP Congestion Control

Prior to KMS 6.7, only WebRTC connections made use of the REMB mechanism, which allows to reduce the sender video bitrate in situations where the network congestion doesn't allow high bitrates to be sent. Now, REMB can also enabled for basic RTP streams.

This means that any REMB-enabled RTP sender will be able to leverage the benefits that this protocol provides for network congestion control.



### Security hardening

*Hardening* is a set of mechanisms that can be activated by turning on several compiler flags, and are commonly used to protect resulting programs against memory corruption attacks. These mechanisms have been standard practice since at least 2011, when the Debian project set on the goal of releasing all their packages with the security hardening build flags enabled ([ref][5-1]). Ubuntu has also followed the same policy regarding their own build procedures ([ref][5-2]).

Kurento Media Server had been lagging in this respect, and old releases only implemented the standard Debian hardening options that are applied by the dpkg-buildflags tool by default:

- Format string checks (`-Wformat -Werror=format-security`).
- Fortify Source (`-D_FORTIFY_SOURCE=2`).
- Stack protector (`-fstack-protector-strong`).
- Read-Only Relocations (*RELRO*) (`-Wl,-z,relro`).

Starting from version 6.7, KMS also implements these extra hardening measurements:

- Position Independent Code (`-fPIC`) / Position Independent Executable (`-fPIE -pie`).
- Immediate Binding (`-Wl,-z,now`).

The PIC/PIE options allow taking advantage of the Address Space Layout Randomization (*ASLR*) protection offered by the Kernel. This protects against Return-Oriented Programming (*ROP*) attacks. However, this technique has an important caveat: it is an all-or-nothing switch, so *all shared objects must be compiled as position-independent code*, and non-PIC plugins will need to be recompiled with `-fPIC` in order to link with Kurento libraries.

For more information about the hardening goals and each of the protection mechanisms that are implemented, check the corresponding section of the Kurento documentation: [Security Hardening][5-3].

[5-1]: https://wiki.debian.org/Hardening#Notes_on_Memory_Corruption_Mitigation_Methods
[5-2]: https://wiki.ubuntu.com/Security/Features#Userspace_Hardening
[5-3]: https://doc-kurento.readthedocs.io/en/latest/dev/hardening.html



### [TODO] New event: MediaTranscodingStateChangeEvent

[TODO]



### [TODO] New sample application: RTP Sender

[TODO]



### [TODO] H.264 support by default

[TODO]
The package `openh264-gst-plugins-bad-1.5`.



# Support services

Kurento is formed by a small team of people. This means that our task pipeline is quite restricted, and most feature or support requests end up being stored in the backlog for a long time. We advance as fast as we can, but time and resources are limited and at the end of the day there is so much that we can do.

If you have some needs that require urgent attention, or want to help with funding development on the Kurento project, we offer consultancy and support services on demand. Please contact us at: [openvidu@gmail.com][6-1].

[6-1]: mailto:openvidu@gmail.com
