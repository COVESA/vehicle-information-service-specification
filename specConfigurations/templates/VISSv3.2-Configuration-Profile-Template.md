<!--
  VISS CONFIGURATION PROFILE TEMPLATE - VISS 3.2
  ------------------------------------------------
  Instructions (delete this comment block when the template is instantiated):
  - Replace every {{PLACEHOLDER}}.
  - For every feature, pick exactly one status from the legend in section 4.
  - A configuration profile may only RESTRICT what the base specification allows.
    It must not add, change, or contradict normative requirements of the base
    specification. If it does, it is an extension, not a configuration profile
    (see section 3).
  - This template contains the feature set of VISS 3.2 (Core, Transport and
    Payload Encoding). Use the template for the VISS version that the
    configuration profile is based on.
  - The feature identifiers used in section 4 are the "Server Feature Naming"
    identifiers from the VISS 3.2 Core appendix "Server Capabilities", so that the
    configuration profile can be mapped directly to a server's Server.Support.*
    declaration. Features without an identifier (marked "none defined") cannot be
    compared with the Server tree.
-->

# {{CONFIGURATION_PROFILE_NAME}} - A VISS Configuration Profile (based on VISS 3.2)

| Field                                  | Value                                              |
|----------------------------------------|----------------------------------------------------|
| Configuration profile name             | {{CONFIGURATION_PROFILE_NAME}}                     |
| Configuration profile identifier       | {{config-profile-id}} (short, lowercase, no spaces) |
| Configuration profile version          | {{X.Y.Z}} (see section 9 for versioning rules)     |
| Short tag (optional)                   | `3.2.0+{{config-profile-id}}.{{N}}` - Optional short label for use in file names, logs and server capability data. It uses SemVer build metadata: the base specification version, followed by `+`, the configuration profile identifier and a revision number. Build metadata is ignored when SemVer determines precedence, so the tag does not imply that the configuration is newer or older than the base specification. The tag is informative only. The configuration profile version above is the authoritative version. |
| Status                                 | Draft / Candidate / Final / Deprecated             |
| Base specification                     | COVESA VISS 3.2 (Core, Transport, Payload Encoding) |
| Compatible base range                  | >= 3.2.0, < 3.3.0                                  |
| Date                                   | {{YYYY-MM-DD}}                                     |
| Owner / Editor(s)                      | {{Organization, name, contact}}                    |
| Location                               | {{URL of this document}}                           |
| License                                | {{license}}                                        |

> VISS 3.2 is the latest version at the time of writing. Set the upper bound of the compatible base range to the next minor version, and widen it only after validation.

---

## 1. Purpose and Scope

{{One or two paragraphs. Why does this configuration profile exist, which use cases and
deployments does it target (in-vehicle server, off-vehicle/cloud server, client
types), and what is explicitly out of scope.}}

## 2. Base Specification and Normative References

This configuration profile is based on, and shall be read together with, the following documents.
The base specification is normative. Where this configuration profile is silent, the base specification applies.

| Document                    | Version | Reference (URL / tag) |
|-----------------------------|---------|-----------------------|
| VISS Core                   | 3.2 | https://github.com/COVESA/vehicle-information-service-specification/releases/tag/v3.2 |
| VISS Transport              | 3.2 | same release |
| VISS Payload Encoding       | 3.2 | same release |
| VISS Implementation Guidelines (informative) | {{version/commit}} | {{URL}} |
| HIM (Hierarchical Information Model) vehicle data profile | {{version}} | {{URL}} |
| VSS (if used)               | {{version}} | {{URL}}               |
| {{Other, e.g. RFCs, customer documents}} | {{}} | {{}}     |

Key words "MUST", "MUST NOT", "SHALL", "SHOULD", "MAY" are used as defined in
RFC 2119 / RFC 8174 when, and only when, they appear in capitals.

## 3. Conformance

### 3.1 Relationship to the base specification

- A server or client that conforms to this configuration profile **MUST** also conform to the base
  specification version stated above.
- This configuration profile **only restricts** optional features, and may narrow parameter ranges
  and set limits. It **does not** add features, change message formats, or alter the
  semantics of any base specification element.
- Any deviation from the above is not permitted in a configuration profile. It requires either a
  contribution to the base specification or a separately declared extension, which
  must be declared in the Server tree as required by the base specification.

### 3.2 Conformance targets

This configuration profile defines requirements for:

- **Server**: {{yes/no}}
- **Client**: {{yes/no}}
- **Other (e.g. gateway, access control servers)**: {{yes/no, specify}}

### 3.3 Conformance claims

An implementation claiming conformance to this configuration profile **MUST** state:
configuration profile identifier and version, base specification version, conformance target
(server/client), and the transport protocol(s) and payload encoding(s) covered.

### 3.4 Declaring the configuration profile in the Server tree (servers)

{{Optional. Describe how a server announces conformance, e.g. an additional
attribute in the Server capability tree. Note that adding a node to the Server
tree is an extension per the base specification, and that the base specification
requires such extensions to be declared in that tree. Alternatively state that
no in-band declaration is required and conformance is declared out of band.}}

## 4. Feature Selection

### 4.1 Status legend

| Status | Meaning for a server                                        | Meaning for a client                                   |
|--------|-------------------------------------------------------------|--------------------------------------------------------|
| **R**  | Required: MUST be supported.                                | MAY rely on it being available.                        |
| **O**  | Optional: MAY be supported. Must be declared if supported.  | MUST NOT rely on it. Must handle absence gracefully.   |
| **X**  | Excluded: MUST NOT be offered when operating under this configuration profile. | MUST NOT use it.                    |
| **M**  | Mandatory in base spec (cannot be changed). Listed for completeness. | Same.                                      |

Rule: a feature that is *optional* in the base specification may be R, O or X here.
A feature that is *mandatory* in the base specification must be M here.

### 4.2 Methods (Core, section "Methods")

The Core text states that transport protocols MUST support the Read and Update
methods, and MAY support the Subscribe, Unsubscribe and Subscription methods.
No Server.Support identifiers are defined for methods.

| Feature                         | Base status | Configuration profile status | Constraints / notes |
|---------------------------------|-------------|------------------------------|---------------------|
| Read, single tree addressability   | Mandatory (Read) | M | Supports wildcards via filters, cannot address signals in multiple trees. {{}} |
| Read, multiple tree addressability | Optional (variant of Read) | {{R/O/X}} | No wildcards, can address signals in multiple trees. {{}} |
| Update, single data             | Mandatory (Update)  | M | {{}} |
| Update, multiple data           | Optional (variant of Update) | {{R/O/X}} | Not supported over HTTP. {{}} |
| Subscribe                       | Optional    | {{R/O/X}} | Not supported over HTTP. {{}} |
| Unsubscribe                     | Optional    | {{R/O/X}} | Must follow Subscribe. |
| Subscription (event messages)   | Optional    | {{R/O/X}} | Must follow Subscribe. |
| Signal Discovery                | Optional    | {{R/O/X}} | Separate request method (alternative to the `metadata` filter). |
| Forest Discovery                | Optional    | {{R/O/X}} | Separate request method (alternative to forest discovery with the `metadata` filter). |

> The Core text states that Read and Update MUST be supported and that each has two variants. It does not
> explicitly state whether both variants are mandatory, and does not list the discovery methods as mandatory
> or optional. The table above treats the first variant as mandatory and the others as optional.
> Confirm this reading with the specification editors before the configuration profile is published.

### 4.3 Filters (identifier = Server.Support.Filter value)

| Identifier  | Feature                                     | Base status | Configuration profile status | Constraints / notes |
|-------------|---------------------------------------------|-------------|------------------------------|---------------------|
| `paths`     | Multiple signal paths                       | Optional | {{R/O/X}} | {{e.g. max number of paths}} |
| `history`   | Historic data access                        | Optional | {{R/O/X}} | {{e.g. max time window}} |
| `timebased` | Time-based event trigger                    | Optional | {{R/O/X}} | {{e.g. min period}} |
| `range`     | Range-based event trigger                   | Optional | {{R/O/X}} | {{single/multi boundary}} |
| `change`    | Change-based event trigger                  | Optional | {{R/O/X}} | {{allowed logic-ops}} |
| `curvelog`  | Curve-logging-based event trigger           | Optional | {{R/O/X}} | {{}} |
| `metadata`  | Metadata access via filter                  | Optional | {{R/O/X}} | Also used for forest discovery (see below). Expected to be deprecated in a coming major version of the base specification (the Signal Discovery and Forest Discovery methods in 4.2 are the alternative). |
| (none defined) | Forest discovery with the filter (a `metadata` request with a path starting with the root node name "HIM") | Optional (part of `metadata`) | {{R/O/X}} | Depends on `metadata`. Same information as the Forest Discovery method in 4.2. |

Filters can be used in Read and Subscribe requests. Subscribe is not supported by the HTTP transport.
The event trigger filters (`timebased`, `range`, `change`, `curvelog`) are used with Subscribe.

### 4.4 Transport protocols (identifier = Server.Support.Protocol value)

| Identifier | Transport              | Base status | Configuration profile status | Constraints / notes |
|------------|------------------------|-------------|------------------------------|---------------------|
| `ws`       | Secure WebSocket       | Optional | {{R/O/X}} | {{port, sub-protocol}} |
| `http`     | HTTPS                  | Optional | {{R/O/X}} | {{port}}. Subscription methods are not supported over HTTP. |
| `mqtt`     | MQTT                   | Optional | {{R/O/X}} | {{topics, QoS}} |
| `grpc`     | gRPC                   | Optional | {{R/O/X}} | {{port}}. Uses Protobuf encoding. |
| `uds`      | Unix Domain Sockets    | Optional | {{R/O/X}} | Socket file named `udsMgr.sock`. The full path is declared in the Server tree. {{}} |

The Transport specification does not mandate a specific transport protocol, but
at least one of the listed transport protocols MUST be supported. The
configuration profile must therefore have at least one of the transports above as R,
or all as O with the requirement that at least one is supported.

### 4.5 Payload encoding (identifier = Server.Support.Encoding value)

| Encoding                    | Base status | Configuration profile status | Constraints / notes |
|-----------------------------|-------------|------------------------------|---------------------|
| JSON (primary payload format) | Mandatory (a client MUST be able to access the payload in JSON format) | M | |
| Protobuf                    | Optional (defined for gRPC, WebSocket and MQTT) | {{R/O/X}} | gRPC always uses Protobuf. {{}} |

### 4.6 Security and access control (identifier = Server.Support.Security value)

| Identifier       | Feature                      | Base status | Configuration profile status | Constraints / notes |
|------------------|------------------------------|-------------|------------------------------|---------------------|
| (none defined)   | Transport security (TLS 1.2) | Mandatory   | M | {{e.g. require TLS 1.3, cipher suites, mutual TLS}} |
| `accesscontrol`  | Access control model         | Optional    | {{R/O/X}} | {{}} |
| `consent`        | Consent support (ECF)        | Optional    | {{R/O/X}} | {{}} |

Access control flows (identifier = Server.Config.AccessControl.Flow value), relevant only if `accesscontrol` is R or O:

| Identifier        | Feature              | Configuration profile status | Constraints / notes |
|-------------------|----------------------|------------------------------|---------------------|
| `short_term`      | Short term flow      | {{R/O/X}} | {{}} |
| `long_term`       | Long term flow       | {{R/O/X}} | {{}} |
| `signalset_claim` | Signal set claim     | {{R/O/X}} | {{}} |

Additional access control constraints (e.g. proof of possession, token lifetimes, purposes and scopes):
{{}}

### 4.7 File transfer (identifier = Server.Support.Filetransfer value)

| Identifier | Feature                     | Base status | Configuration profile status | Constraints / notes |
|------------|-----------------------------|-------------|------------------------------|---------------------|
| `download` | File download (to vehicle)  | Optional | {{R/O/X}} | {{max size, formats}} |
| `upload`   | File upload (from vehicle)  | Optional | {{R/O/X}} | {{max size, formats}} |

### 4.8 Data compression (identifier = Server.Support.DataCompression value)

| Identifier       | Feature                          | Base status | Configuration profile status | Constraints / notes |
|------------------|----------------------------------|-------------|------------------------------|---------------------|
| `pathuid`        | Static UID path compression      | Optional | {{R/O/X}} | {{}} |
| `pathlocal`      | Request local path compression   | Optional | {{R/O/X}} | {{}} |
| `timestamplocal` | Response local timestamp compression | Optional | {{R/O/X}} | {{}} |

### 4.9 Data model and trees

VISS 3.2 uses the rule sets of the HIM vehicle data profile for the content of the trees. A server may manage a set of trees (a forest).

| Item                                    | Configuration profile requirement |
|-----------------------------------------|-----------------------------------|
| Vehicle tree root node name             | {{e.g. "Vehicle"}} (base: should be "Vehicle", required for VSS compatibility) |
| Signal catalogue / signal subset        | {{Reference to VSS version and list/file of included signals, or "all"}} |
| Datatype definition tree                | {{required / not applicable}} (base: mandatory if the vehicle tree contains struct definitions or references to allowed definitions; root node name starts with "Types") |
| Struct datatypes allowed                | {{yes/no, which}} |
| Multiple vehicle trees (forest)         | {{allowed / not allowed}} |
| Path delimiter                          | {{"." only / "/" allowed (HTTP)}} (base: "." recommended, "/" supported) |
| Server capabilities tree (Server)       | M (as defined in the base specification, exactly one tree, root node name "Server") |

Signal-level access rules that the configuration profile imposes (e.g. read-only signals,
signals requiring access control):
{{}}

### 4.10 Other optional behaviours

| Feature                                                             | Base status | Configuration profile status | Constraints / notes |
|---------------------------------------------------------------------|-------------|------------------------------|---------------------|
| In-line error reporting (`viss-inline:Data-not-available`) for multiple-signal requests, instead of a 404 error | Optional (server MAY) | {{R/O/X}} | {{}} |
| Timestamp-based discarding of out-of-order Update requests | Optional (server MAY) | {{R/O/X}} | {{e.g. sliding window size}} |

## 5. Parameter Constraints and Limits

Restrictions on values that the base specification leaves open.
All of these must be a subset of what the base specification permits.

| Parameter                                   | Constraint |
|---------------------------------------------|------------|
| Max concurrent subscriptions per client     | {{}} |
| Min `timebased` period (ms)                 | {{}} |
| Max number of paths in a request            | {{}} |
| Max history time window                     | {{}} |
| Max message / payload size                  | {{}} |
| Timestamp resolution                        | {{e.g. at least milliseconds (base: at least seconds)}} |
| Request timeout / response time target      | {{}} |
| `requestId` format                          | {{integer / UUID / either}} (base allows both) |
| Port numbers                                | {{or "as recommended in base specification"}} (HTTP 443, WebSocket 6443, MQTT 8883, gRPC 5443, AGT server 7443, AT server 8443; non-normative in the base specification) |
| {{Other}}                                   | {{}} |

## 6. Error Handling

The base specification requires a server to support the status codes, reasons and
descriptions listed in the Transport specification, section "Status Codes" (400 bad_request,
400 invalid_data, 401 invalid_token, 403 forbidden_request, 404 unavailable_data, 408 request_timeout,
429 too_many_requests, 502 bad_gateway, 503 service_unavailable, 504 gateway_timeout), across all
supported transport protocols.

{{State any restrictions on which error numbers/reasons from the base
specification the configuration profile uses or requires in specific situations. Do not
define new status codes here. If the configuration profile needs a new code, it is an
extension.}}

## 7. Implementation Requirements (Optional)

{{Non-VISS requirements that the configuration profile owner wants to attach, kept clearly
separate from the conformance rules above. For example: performance targets,
deployment topology, logging, certification process. Mark as informative if not
testable against the VISS messages.}}

## 8. Conformance Test Plan (Optional)

| Test ID | Feature / requirement | Description | Expected result | Applies to (server/client) |
|---------|-----------------------|-------------|-----------------|----------------------------|
| {{T-001}} | {{}} | {{}} | {{}} | {{}} |

{{Reference to test suite / tool, if any.}}

## 9. Versioning and Maintenance

### 9.1 Configuration profile version

The configuration profile uses Semantic Versioning 2.0.0 (MAJOR.MINOR.PATCH) for **its own** version,
independent of the base specification version.

| Change                                                                                   | Version increment |
|------------------------------------------------------------------------------------------|-------------------|
| Editorial fixes, clarifications that do not change conformance                           | PATCH |
| Relaxing a restriction (e.g. X -> O, or a looser limit), such that every previously conformant implementation stays conformant | MINOR |
| Tightening a requirement (O -> R, O -> X, R -> X, stricter limits), such that a previously conformant implementation may no longer be conformant | MAJOR |
| Moving to a new base specification MINOR version, with no change to the feature selection | MINOR |
| Moving to a new base specification MAJOR version                                          | MAJOR |

> Note on the MINOR/MAJOR rule: decide and state precisely whether the compatibility
> viewpoint is the server's or the client's. Relaxing a restriction for servers (X -> O)
> is backward compatible for existing servers but may break clients that relied on the
> feature being absent, and tightening (O -> R) breaks existing servers. Adjust the
> table above to the compatibility guarantee the configuration profile owner wants to give.

### 9.2 Relationship between configuration profile version and base version

- The "Compatible base range" in the header states which base versions the configuration profile has been
  validated against.
- A new patch release of the base specification within the compatible range does not
  require a new configuration profile version.
- Support of a newer base version requires a configuration profile release that states it.

### 9.3 Change process and deprecation

{{How changes are proposed and approved, the notice period for MAJOR changes, how long
a superseded configuration profile version stays supported.}}

## 10. Revision History

| Configuration profile version | Date | Base version | Summary of changes | Author |
|-------------------------------|------|--------------|--------------------|--------|
| {{1.0.0}}       | {{YYYY-MM-DD}} | 3.2 | Initial version | {{}} |

## Appendix A. Configuration Profile Summary (Quick Reference)

| Area                | Required (R)          | Optional (O) | Excluded (X) |
|---------------------|-----------------------|--------------|--------------|
| Methods             | {{}}                  | {{}}         | {{}}         |
| Filters             | {{}}                  | {{}}         | {{}}         |
| Transports          | {{}}                  | {{}}         | {{}}         |
| Payload encodings   | {{}}                  | {{}}         | {{}}         |
| Security            | {{}}                  | {{}}         | {{}}         |
| File transfer       | {{}}                  | {{}}         | {{}}         |
| Data compression    | {{}}                  | {{}}         | {{}}         |

## Appendix B. Machine-readable Configuration Profile (Optional)

Optional YAML form of section 4, useful for tooling and for comparing against a
server's `Server.Support.*` data.

```yaml
configuration_profile:
  id: {{config-profile-id}}
  version: {{1.0.0}}
  short_tag: "3.2.0+{{config-profile-id}}.{{N}}"
  base: { name: VISS, version: "3.2", compatible: ">=3.2.0 <3.3.0" }
  features:
    methods:
      read_single_tree:   M
      read_multiple_tree: {{R|O|X}}
      update_single:      M
      update_multiple:    {{R|O|X}}
      subscribe:          {{R|O|X}}
      signal_discovery:   {{R|O|X}}
      forest_discovery:   {{R|O|X}}
    filter:
      paths:     {{R|O|X}}
      history:   {{R|O|X}}
      timebased: {{R|O|X}}
      range:     {{R|O|X}}
      change:    {{R|O|X}}
      curvelog:  {{R|O|X}}
      metadata:  {{R|O|X}}
    protocol:
      ws:   {{R|O|X}}
      http: {{R|O|X}}
      mqtt: {{R|O|X}}
      grpc: {{R|O|X}}
      uds:  {{R|O|X}}
    encoding:
      protobuf: {{R|O|X}}
    security:
      accesscontrol: {{R|O|X}}
      consent:       {{R|O|X}}
    filetransfer:
      download: {{R|O|X}}
      upload:   {{R|O|X}}
    datacompression:
      pathuid:        {{R|O|X}}
      pathlocal:      {{R|O|X}}
      timestamplocal: {{R|O|X}}
  limits:
    max_subscriptions: {{}}
    min_timebased_period_ms: {{}}
```
