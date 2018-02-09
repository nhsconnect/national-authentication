---
title: Smart on FHIR
keywords: homepage
sidebar: overview_sidebar
permalink: TechOverview_SmartOnFHIR.html
toc: true
summary: An overview of Smart on FHIR.
---

SMART, which is an acronym for "Substitutable Medical Applications, Reusable Technologies", was born in 2010 and is run out of the Boston Children’s Hospital Computational Health Informatics Program and the Harvard Medical School Department of Biomedical Informatics. 

The SMART on FHIR standard grew out of the wider SMART work. It is a relatively simple standard, and is currently going through the process of being balloted to be adopted as a HL7 standard. The full details of the standard are set out on the [SMART on FHIR website](http://docs.smarthealthit.org/){:target="_blank"}.

The standard complements the FHIR standard by providing a standardised approach for:

- Authorisation using OAuth: By providing a standard structure for the OAuth Scopes, linked to FHIR resources and operations
- Launching "apps" from an EPR, passing across the patient and user/security context to allow simpler integration for app developers

The national authorisation services will aim to align with the Authorisation aspects of the SMART on FHIR standard.

The OAuth and OpenID Connect standards provide a robust, standardised way of authenticating and authorising users for access to resources. This allows standard tools and libraries to be used in both clients and servers for handling these interactions. The standard does however require the implementor to define the attributes of a user, and the types of resources in their system that they want to authorise access to. This is fine for individual system authorisation, but it means that clients and servers have to agree some of these basic attributes before they can successfully authenticate and authorise users. When considering a standard that could be applied across a wide range of health and care systems, there is a need to consider standardising these attributes to allow more general identity and authorisation solutions to be developed, and used across a range of systems without requiring clients to make changes to understand different attributes for each new service they want to integrate with.

## Use of Scopes ##

In OAuth, a request for authorisation includes one or more "scopes" - these identify the type of resources and operations the client wants to be authorised to access. OAuth itself leaves the structure and content of these scopes open to the implementor to define, and the SMART on FHIR standard defines a standard syntax for scopes that relate to FHIR resources.

The specific structure and syntax of the scopes proposed is defined [here](http://docs.smarthealthit.org/authorization/scopes-and-launch-context/){:target="_blank"}.

It is worth noting that the SMART on FHIR scopes are deliberately minimal - they are intended to cover the majority of simple use-cases, but there is likely to be some use-cases where a more complex set of permissions is needed. Each nationally defined FHIR API will align wherever possible, but where additional scopes are needed these will be specified in the specification for that API. For example, if a FHIR endpoint included a set of Observation resources about a patient - including some clinical observations and some non-clinical - there is no easy way of specifying that a user is authorised to access the non-clinical Observation resources but not the clinical ones. In cases like this, the additional Scopes will be specified in the relevant API specification.

## Alignment with RBAC ##

The national authorisation services are likely to use the national RBAC roles and activities associated with authenticated users to inform it's authorisation decisions. This means that the granting of specific scopes will be linked to the role the user is in. The specific mapping between the RBAC model and the scopes for a specific API will be defined in the relevant API specifications.
