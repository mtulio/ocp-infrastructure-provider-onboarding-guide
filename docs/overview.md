# Overview

This document provides a high level view of the workflow for adding a new
infrastructure provider to OpenShift. The following list is meant to give
a general idea of the work involved with this process, the links contained
within the list reference documents with greater detail for each step.

## Workflow

1. [Preparation](/preparation)

    Start with an idea to add a new infrastructure provider to OpenShift.
    Identify contacts within Red Hat, and the community, and then set
    expectations about the process ahead.

1. [Information Gathering](/information-gathering)

    Define the reference architecture and toplogy for OpenShift clusters
    on the new provider. Inventory existing components including licenses
    and plugin providers, and identify supported formats and infrastructure.

1. [OpenShift Enhancement](/openshift-enhancement)

    Create an enhancment describing the new platform in detail, this will
    become a part of the official
    [OpenShift enhancements](https://github.com/openshift/enhancements).

1. [Cloud Controller Manager](/cloud-controller-manager)

    New providers must have a
    [Cloud Controller Manager](https://kubernetes.io/docs/concepts/architecture/cloud-controller/)
    integrated into OpenShift, including a repository in the OpenShift
    organization and container images included in the release payload.

1. [Container Storage Interface Driver](/container-storage-interface-driver)

    Providers that expose storage options must have a CSI driver integrated into
    OpenShift, including a repository in the OpenShift organization and container
    images inclujded in the release payload.

1. [Machine API Controllers](/machine-api-controllers)

    New providers must have a Machine actuator, and related controllers, for
    the [Machine API Operator](https://github.com/openshift/machine-api-operator),
    including a repository in the OpenShift organization and container images
    included in the release payload.

1. [Network Ingress and DNS](/network-ingress-dns)

    Evaluate provider-specific support for ingress load balancers and endpoint
    publishing strategies, as well as internal and external DNS support.
    Update and validate the
    [Cluster Ingress Operator](https://github.com/openshift/cluster-ingress-operator)
    for the new infrastructure provider.

1. [Continuous Integration and Testing](/continuous-integration-and-testing)

    All components must have a suite of automation including unit style testing
    (run in isolation), and integration testing (run on cluster from the
    provider). This automation is part of the OpenShift development and release
    process, and exists within the OpenShift organization.

1. [Component Infrastructure](/component-infrastructure)

    Once OpenShift can be installed and operated on the new infrastructure
    platform attention should be given to the dynamic infrastructure services.
    These components are non-critical to the installation process and include
    things like the image registry.

1. [Documentation](/documentation)

    Product documentation is required for installation and maintenance tasks
    on the new infrastructure platform. Source level documentation is expected
    for all component repositories added to the OpenShift organization.

1. [Red Hat Relationship](/red-hat-relationship)

    After the new infrastructure provider is ready for release, what are the
    commitments around maintenance and future releases.

1. [Release](/release)

    What to do once the code is approved and the release is ready for public
    consumption. How to promote and advertise, and work with Red Hat.

## Integration Map

Dynamic map of base components in a cloud provider in a basic IPI integration.

<div>
<div class="mxgraph" style="max-width:100%;border:1px solid transparent;" data-mxgraph="{&quot;highlight&quot;:&quot;#0000ff&quot;,&quot;nav&quot;:true,&quot;resize&quot;:true,&quot;toolbar&quot;:&quot;zoom layers tags lightbox&quot;,&quot;xml&quot;:&quot;&lt;mxfile host=\&quot;app.diagrams.net\&quot; modified=\&quot;2021-09-29T21:16:37.559Z\&quot; agent=\&quot;5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36\&quot; etag=\&quot;ZAl17RiUS17eI2W5A_UQ\&quot; version=\&quot;15.2.2\&quot; type=\&quot;google\&quot;&gt;&lt;diagram name=\&quot;OCP_Components_Overview\&quot; id=\&quot;zqqOIAfYTedYN5DSwbxW\&quot;&gt;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&lt;/diagram&gt;&lt;/mxfile&gt;&quot;}"></div>
<script type="text/javascript" src="https://viewer.diagrams.net/js/viewer-static.min.js"></script>

</div>
