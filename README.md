rancher-traefik
==============

This image is the traefik dynamic conf for rancher. It comes from [rawmind/rancher-tools][rancher-tools].

## Credits

This work is based on [rawmind/racher-traefik](https://github.com/rawmind0/rancher-traefik).

## Certificates

Default Traefik certificate is added to the image. When ACME is enabled the certificates will be overruled.

## Usage

This image has to be run as a sidekick of [rawmind/alpine-traefik][alpine-traefik], and makes available /opt/tools volume. It scans from rancher-metadata, looking for services and externalServices that has traefik labels, and generates traefik frontend and backends to expose the services.

## Configuration labels

Traefik labels, has to be created in your service or externalService, in order to get included in traefik dynamic config. 

- traefik.enable = < true | stack | false > #Controls if you want to publish or not the service
  - true: the service will be published as *service_name.traefik_domain*
  - false: the service will not be published
- traefik.service = < service > # Overrides the service_name
- traefik.domain = < domain.name >	# Domain names to route rules. Multiple domains separated by ","
- traefik.port = < port > # Port to expose throught traefik
- traefik.acme = < true | false >	# Enable/disable ACME traefik feature

WARNING: Only services with healthy state are added to traefik, so health checks are mandatory.

[alpine-traefik]: https://github.com/rawmind0/alpine-traefik
[rancher-tools]: https://github.com/rawmind0/rancher-tools
