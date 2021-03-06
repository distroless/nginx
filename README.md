# nginx

`distroless.dev/nginx` is a minimal nginx base image rebuilt every night from source.

The image is currently built for `amd64`, `arm64` and `armv7` architectures.
If you'd like to see other architectures supported, please file an issue!

## Usage

To try out the image, run:

```
docker run -p 8080:80 distroless.dev/nginx
```

If you navigate to `localhost:8080`, you should see the nginx welcome page.

To run an example Hello World app, navigate to the root of this repo and run:

```
docker run -v $(pwd)/examples/hello-world/site-content:/var/lib/nginx/html -p 8080:80 distroless.dev/nginx
```

If you navigate to `localhost:8080`, you should see `Hello World from Nginx Distroless!`.


## Signing

All distroless images are signed using [Sigstore](https://sigstore.dev)!
To verify an image, download [cosign](https://github.com/sigstore/cosign) and run:

```
COSIGN_EXPERIMENTAL=1 cosign verify distroless.dev/nginx | jq

Verification for distroless.dev/nginx:latest --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - Any certificates were verified against the Fulcio roots.
[
  {
    "critical": {
      "identity": {
        "docker-reference": "ghcr.io/distroless/nginx"
      },
      "image": {
        "docker-manifest-digest": "sha256:3b28db71687f52741598f4f68d2e4bea8ee86db57d7394337118316d1f4c8b9f"
      },
      "type": "cosign container image signature"
    },
    "optional": {
      "Issuer": "https://token.actions.githubusercontent.com",
      "Subject": "https://github.com/distroless/nginx/.github/workflows/release.yaml@refs/heads/main",
      "run_attempt": "1",
      "run_id": "2626578822"
      ...
    }
  }
]
```

You can verify that the image was built in Github Actions in this repository from the `Issuer` and `Subject` fields.

## Development

To develop this image or build it locally, see [DEVELOPMENT.md](./DEVELOPMENT.md).
