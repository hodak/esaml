## Changelog

All changes are in the `main` branch (`master` remains unchanged).

### v4.1.0

+   Support for Encrypted Assertions - PR #13 from [tcrossland](https://github.com/tcrossland)
    Includes support for `aes128-gcm`, `aes128-cbc` and `aes256-cbc` data encryption algorithms
    and `rsa-oaep-mgf1p` key encryption algorithm.

### v4.0.0

+   Fixed issue: #11 - Support for Cowboy 2
    
### v3.6.1

+   Fixed issue: #9 - HTTP-REDIRECT wrong case
    Corrected SP metadata XML generated by `esaml` - `HTTP-Redirect` instead of
    the full uppercase form. Reported by [mikegazdag](https://github.com/mikegazdag).

### v3.6.0

+   Fixed issued: #8 - LogoutRequest Validation Error
    Removed `ProtocolBinding` attribute from `LogoutRequest` and `LogoutResponse`.
    Made sure the `saml:Issuer` element is in proper sequence in the requests.
    Schema validation was failing for `LogoutRequest` and `LogoutResponse` without
    these fixes. Thanks to [mjcloutier](https://github.com/mjcloutier) for reporting
    this issue.

### v3.5.0

+   Erlang/OTP 21.0 support
    Removed tuple calls. Thanks to PR from [zwilias](https://github.com/zwilias).

### v3.4.0

+   Fixed issue: #4 - InResponseTo - make this available
    In case of SP initiated SSO, the auth response includes the original
    request ID. Make this available in the assertion subject esaml record.
    (as `in_response_to`). The IDP initiated requestes don't include this.
    The `in_response_to` field is set to an empty string in that case.

### v3.3.0

+   `NameID` format can be passed as a parameter to `esaml_sp:generate_authn_request/3`.
    Deprecated `esaml_sp:generate_authn_request/2`. Pass in `undefined` as NameID format
    if you do not want to pass in `NameIDPolicy` in the authn request.

+   Passing `#esaml_subject{}` with the values returned in the authn response
    assertion subject. This is essential for sending appropriate `NameQualifier`,
    `SPNameQualifier` and `Format` values in the SLO logout request. Without these
    values, Shibboleth fails to match the SP session on the IdP side. Deprecated
    `esaml_sp:generate_logout_request/3`. It will be removed in a future relase.

### v3.2.0

+   Generate SP Metadata XML that passes schema validation

### v3.1.0

+   Support for customizable SP entity_id