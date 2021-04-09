---
layout: page
title: Bootfiles
permalink: /documentation/config/bootfiles
parent: Configuration
grand_parent: Documentation
---

# Bootfiles

Bootfiles are defined in **[bootfile_\<bootfile_name>]** sections. _\<bootfile>_ is an arbitrarily chosen identifier like _efi32_, _bios_ or _efi64_. Each bootfile can be restricted to an architecture and/or an user class which is sent by the PXE client.

The **bootfile URL** must have a format like _\<protocol>://[\<address>]/\<file>_. The possible protocols are dependent on the PXE client. TFTP should be supported by almost every client.

```ini
bootfile_url = tftp://[fd00::1]/pxe.efi
```

Optionally restrict the bootfile to a specific **client CPU architecture**. If the client doesn’t match the requirement, the next bootfile assigned to the class definition is chosen or no bootfile is provided, if there are no further alternatives.

Either the integer identifier for an architecture is possible (e.g. 0009 for EFI x86-64). The integer must consist of four numeric digits. Empty digits must be zerofilled (e.g. 9 -> 0009). For a full list of possible integer identifiers see [RFC 4578 section 2.1](https://tools.ietf.org/html/rfc4578#section-2.1). Alternatively the well-known names of registered CPU architectures can be used:

- Intel x86PC
- NEC/PC98
- EFI Itanium
- DEC Alpha
- Arc x86
- Intel Lean Client
- EFI IA32
- EFI BC
- EFI Xscale
- EFI x86-64

The parameter **client_architecture** looks like this:

```ini
client_architecture = Intel x86PC
```

Optionally restrict this bootfile to PXE clients sending this **user class**. It is matched against the value of the client with simple comparison (no regular expression):

```ini
user_class = iPXE
```

This restricts the bootfile to the iPXE boot firmware.
