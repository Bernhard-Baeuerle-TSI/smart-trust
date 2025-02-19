\#\# Onboarding Checklist

\#\#\# General Hints

This document describes the standard onboarding process (so called Future Onboarding Process - FOP).

\*\*Note:\*\* In the embedded image the following relabels apply:

\* DCCG -\> TNG

\* CSCA -\> SCA

\* DCC -\> VDHC (Verifiable Digital Health Certificate)

\* NB -\> TNP

It is highly recommended:

\- \*\*to use certificates issued from a public CA which follows the CAB Forum Rules\*\*

\- \*\*not to reuse any certificates across the different staging environments\*\*

\#\# Procedure

In the following description the required steps are divided into three sections:

[1] - [] - Application and Verification  
[30] - [] Setup  
[50] - [End] Onboarding

\#\#\# Application and Verification

[1] The eligible Trust Network Participant (TNP) has to submit its [link to the form. [Document 5] ] to tng-support@who.int .

[2 – 3] WHO validates all provided data and verify that such a data follows WHO compliance with Trusted Network Terms of Participation (TOP 0 – 3)as well as: ´s eligibility criteria, governmental entity/health agency, contact details of approvers and individuals.

\< see chapter 9.5 in TOP details \>

[4 - 5] In case no compliance with WHO governance rules is given, the application is rejected. The rejection is communicated to the TNP by email.

[6] TNP needs to modify the data they shared with WHO and re-apply it.

[7] If the WHO’s technical team gives a positive opinion, the eligible Trust Network Participant will be invited to start the onboarding process. The following information is included:

1.  The necessary technical specifications and configuration information to connect the local backend systems to the WHO TNG
    1.  The request to provide the necessary information to be onboarded to the different environments (UAT, PROD, DEV (optional))
    2.  The request to comply with the Trust Network Terms of Participation

[8] The TNP receives the confirmation and necessary technical information to connect to the TNG and register the certificates.

For a successful connection to the gateway there are the following steps [9] – [11] to prepare:

[9] Create certificates per environment

1) Certificates must be prepared for all environments (self-signed allowed) following the requirements in Certificate Governance - Authentication: TNPTLS - Upload: TNPUP - SCA(s): TNPSCA

2) Prepare public keys in PEM format in your private GitHub repository (see [11]) dedicated to environment keys.

3) The prepared public keys must be tagged by the generated GPG keys:

1.  Tag the version of your latest information by using git tag + signing commands either from terminal or developer IDE. Please note that an update in GitHub web desktop itself is not working, because the platform will use an intermediate key.
2.  The bot user clones the latest tag of your private repo and verifies the signature of the tag against the onboarded GPG keys
3.  After verification the content will be taken over for

[10] Create the GPG keys per environment and per each user needed.

Follow the [instructions](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) to create a key: https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key

Use Algorithm RSA or EC with minimum key length of 4096 bit (RSA) or 256 bit (EC).

[11] The TNP creates the private GitHub repositories per environment

1.  [Create a private git repository on GitHub](https://docs.github.com/en/get-started/quickstart/create-a-repo).
2.  Prepare the following information to be provided in the onboarding request:
    -   Environment repository URL’s (all private to hide uploader's identity) (DEV (optional), UAT, PROD)
    -   Invite the WHO bot user to the private repository (with read rights). The bot user is: tng-bot for PROD and tng-bot-dev for DEV (optional) and UAT environments.

[12] Upon GitHub repository creation and invitation to GitHub bot user to WHO is sent, validity for accepting this invitation is 7 days by default. If no action is taken it loses validity.

[13] Invitation for GitHub bot user must be accepted by WHO within 7 days since invitation was emitted.

[14] TNP is ready for onboarding according to WHO requirements and governance and has collected the following information in the :

\- the URL of the private GitHub repositories for each environment (UAT, PROD, DEV (optional))

\- the GPG keys per environment and authorized/responsible person

\- 3-digit ISO code

TNP exchanges the Letter of Application to WHO.

[15] The is received. In case the TNP hasn’t requested the Transitive Trust (only EU DCC members) or the requirements are NOT fulfilled, then await confirmation through either of channels; otherwise if Transitive Trust requirement is fulfilled and Transitive Trust is requested by a EU DCC member follow to step [30].

Find detailed information about the Transitive Trust [here.](https://github.com/WorldHealthOrganization/smart-trust/blob/main/input/pagecontent/concepts_onboarding.md#transitive-trust-on-boarding-process)

[16 - 17] The validation and confirmation of the provided GPG keys takes place through either of channels:

1.  Through a Face to Face meeting
2.  Through Diplomat Channel signed confirmation
3.  

When the Letter of Application is received, identification of individuals take place with passport, finger printing.

[18] WHO acknowledges the Letter of Application and proceeds to validate the provided GPG key(s) and email address(es). At this stage verification of rules compliance takes place. Verification is in detailed according to process and individuals involved in the request.

[19] In case the compliance rules verification failed, WHO need to inform the TNP by email.

[20] The TNP receive an email with information indicating that validations failed. Corrective activities have to be taken.

[21] WHO is checking if the given email address is included in the provided GPG key.

[22] Validate that GPG key matches cryptographic/governance criteria

\- Key length (min. 3072 bit for RSA and min. 256 bit for ECDSA)

\- mail address in GPG key must match with the provided mail address in the Letter of Application

[23] WHO is collecting the required information to be provided to the operations team (OPS):

\- GPG keys of all confirmed people and for all requested environments (UAT, PROD and optional DEV)

\- the URL's of the applicant private GitHub repositories

\- 3-digit ISO code

\#\#\# Setup

[30] The collected onboarding information is sent to the operations (OPS) team. The onboarding (OB) team is informed as well.

[31 - 35] The onboarding data is taken over to the configuration files by the service provider to automate the GitHub processes. As a result, a Pull Request (PR) is created. Dependent on the environment, the subsequent steps differ.

[38] For UAT (and optional DEV), an auto signing process signs the keys.

[36 -37] For PROD environment, the PR is verified by WHO. After successful verification, the air-gapped signing process is performed to sign the keys.

[39] The service provider checks the PR as well.

[40 - 41] In case the verification failed, WHO is informed about the outcome.

[42] In case the verification was successful the whitelisting of the certificates is initiated.

[43 - 45] and the participant will be informed that the preparation has been completed successfully.

\#\#\# Onboarding

[50] The participant is connecting to UAT environment and the following steps has to be performed to check the connection:

1) check the connectivity with the following command:  
curl -v https://tng-uat.who.int/trustList --cert TLS.pem --key TLS_key.pem  
You should see a output like:

\`\`\`

[

{

"kid": "+jrpHSqdqZY=",

"timestamp": "2023-05-25T07:55:21Z",

"country": "XC",

"certificateType": "UPLOAD",

"thumbprint": "fa3ae91d...",

"signature": "MIAGCSqGSIb3D...",

"rawData": "MIIErTCCA5WgAwIBAgII..."

}

]

\`\`\`

2) Test the other Trustlist Routes in the same style (e. g. with DSC/SCA/Upload/Authentication…)

[51] In case the connection fails, some corrective actions must be performed to analyze and solve the issue(s). The operations team is supporting the TNP.

[52] After the connection to the TNG is established the participant can start the dry run test on UAT.

This test includes the listed steps:

\- Upload one or more DSC's to the TNG (Details: xyyy)

\- Delete at least one DSC again (Details: xyyy)

\- Upload it again if it is required for further testing

\- Download the trust list from gateway

\- Provide sample DCC's to be verified by the service provider

\- Validate some sample DCC's to ensure the validation implementation is working fine

[53] After executing all required steps, the participant must provide the test results to the service provider.

[54 - 55] The service provider checks the results

[56] and in case of any issues additional corrective actions are bespoken and solved with the participant.

[] the participant is allowed to connect to TNG PROD environment (for detailed information see [50]).

[] In case the connection fails, some corrective actions must be performed to analyze and solve the issue(s). The operations team is supporting the TNP.

[] After the connection to the TNG PROD is established the Production Readiness Test can start.

This test includes the listed steps:

a) Create a Document Signer Certificate (DSC) and sign it by the SCA

b) Create an CMS package with the following command:

openssl x509 -outform der -in cert.pem -out cert.der

openssl cms -sign -nodetach -in cert.der -signer signing.crt -inkey signing.key -out signed.der -outform DER -binary

openssl base64 -in signed.der -out cms.b64 -e -A

Note: cert.der is your DSC, signing.crt is the TNPUP

c) Upload the CMS package to the gateway  
curl -v -X POST -H "Content-Type: application/cms" --cert TLS.pem --key TLS_key.pem --data @cms.b64 https://tng-uat.who.int/signerCertificate  
d) Download the trustlist again and check if your DSC is available.

**Note**: Some versions of curl don’t attach the client certificates automatically. This can be checked via curl –version. Ensure that the used version is linked to OpenSSL. Especially under Windows (https://curl.se/windows/):  
  
OpenSSL Test Example (working)

e) Delete at least one DSC again [Details to be entered]

f) Upload it again in case the DSC is required

[6 - 6] After executing all required steps, the participant must provide the test results to the service provider by mail.

[6] The service provider checks the results.

[6] and in case of any issues additional corrective actions are bespoken and solved with the participant.

[6 - ] After passing the Production Readiness Test, the participant is allowed to use the TNG PROD environment. A confirmation email is sent to the participant and to WHO with the confirmation about the successfully passed test and the completion of the onboarding process.

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* older content follows \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

\#\#\# [optional] Onboarding to the Development Environment (DEV) [do we need this part of the description for the DEV?]

Onboarding to the DEV environment isn't a must and is only performed on request from the participant.

Please follow the instructions according to the UAT onboarding process describe below.

1) Prepare public keys in PEM format in a private Github repository dedicated to development environment keys. Follow the procedure described in this Github repository: https://github.com/WorldHealthOrganization/tng-participant-template.

2) After onboarding succeeded connect your development setup as described below in the next section "Onboarding to the User Acceptance Test Environment (UAT)".
