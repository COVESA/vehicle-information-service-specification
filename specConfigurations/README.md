# VISS Configuration Profiles

This folder contains **configuration profiles** for the Vehicle Information Service Specification (VISS).

A configuration profile is a named and versioned selection of the optional features of a specific VISS
version. It lets an organization state "we use VISS 3.1, restricted to this feature set" and refer to
that configuration with a version number, without changing the VISS specification itself.

A configuration profile can only restrict what the base specification allows. It does not add features,
change message formats or alter the semantics of the base specification. A server that conforms to a
configuration profile therefore also conforms to the VISS version it is based on.

> **Terminology.** From VISS 3.3 the base specification also uses the word *profile* for the HIM information
> profiles (VehicleData profile and Data profile). These are unrelated to configuration profiles.

## Folder structure

```
specConfigurations/
  README.md
  templates/
    VISSv3.0-Configuration-Profile-Template.md
    VISSv3.1-Configuration-Profile-Template.md
    VISSv3.2-Configuration-Profile-Template.md
    VISSv3.3-Configuration-Profile-Template.md
  <completed configuration profiles>
```

Completed configuration profiles are stored directly in this folder. The blank templates are stored in
`templates/`.

## Creating a configuration profile

1. **Pick the template for the VISS version you base the configuration profile on.** Each template contains
   the feature set of exactly that version, so the choice determines which features can be selected.

   | Template | Differences compared with the previous version |
   |----------|-----------------------------------------------|
   | v3.0 | Baseline for the templates. Uses the VSS rule set, no forest concept. |
   | v3.1 | HIM vehicle data profile rule set, forests of trees, forest inquiry, Unix Domain Sockets, Update `timestamp`. |
   | v3.2 | Multiple tree Read, multiple data Update, Signal Discovery and Forest Discovery methods. |
   | v3.3 | HIM Data profile support, `Server.Support.Profile` in the Server tree. |

2. **Copy the template** to this folder and rename it (see the naming convention below).
3. **Fill in the document.** Replace every `{{PLACEHOLDER}}`, select R (required), O (optional), X (excluded)
   or M (mandatory in the base specification) for every feature, and remove the instruction comment at the top.
4. **Choose the version numbers.** The configuration profile has its own Semantic Versioning 2.0.0 version
   (`MAJOR.MINOR.PATCH`) that is independent of the base specification version. The optional short tag
   `<base version>.0+<config-profile-id>.<N>` is informative only. Section 9 of the template describes when
   each part is incremented.
5. **Check the result** against the Server tree of an implementation. The feature identifiers in section 4 of
   the templates are the same as the `Server.Support.*` values defined by the base specification.

## Naming convention

Completed configuration profiles are named

```
<organization>-VISSv<base version>-Configuration-Profile.md
```

for example `Acme-VISSv3.1-Configuration-Profile.md`. If several versions of the same configuration profile
must be kept, either keep them in version control history, or append the configuration profile version:
`Acme-VISSv3.1-Configuration-Profile-1.2.0.md`.

The base version in the file name is the VISS version the configuration profile is based on, not the
version of the configuration profile.

## Maintaining the templates

- A template must follow its base specification. If a VISS version is corrected or re-released, check the
  corresponding template against it.
- The `VISSv3.3` template was written against the `v3.3` branch (identical to the `v3.3rc0` tag). Check it
  against the final v3.3 release.
- When a new VISS minor or major version is released, create a new template for it by comparing the
  Core, Transport and Payload Encoding documents with the previous version, and add its row to the table above.
- Fixes that apply to all versions must be applied to every template.
