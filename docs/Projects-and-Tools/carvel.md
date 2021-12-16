# Carvel Tool Suite

It is a suite of tools that provides a set of reliable, single-purpose, composable tools that aid in your application building, configuration, and deployment to Kubernetes.

[Carvel Tools Home](https://carvel.dev/)

## ytt

- ytt is a command-line tool used to template and patch YAML files. It also provides the means to collect fragments and piles of YAML into modular chunks for easy re-use.
- [Docs are here](https://carvel.dev/ytt/docs/latest/)

## kapp

- kapp (pronounced: kap) CLI encourages Kubernetes users to manage resources in bulk by working with “Kubernetes applications” (sets of resources with the same label). It focuses on resource diffing, labeling, deployment and deletion.
- [Docs are here](https://carvel.dev/kapp/docs/latest/)

## kbld

- kbld (pronounced: kei·bild) seamlessly incorporates image building and image pushing into your development and deployment workflows.
- [Docs are here](https://carvel.dev/kbld/docs/latest/)

## imgpkg

- imgpkg is a tool that allows users to store a set of arbitrary files as an OCI image. One of the driving use cases is to store Kubernetes configuration (plain YAML, ytt templates, Helm templates, etc.) in OCI registry as an image.
- [Docs are here](https://carvel.dev/imgpkg/docs/latest/)

## vendir
- vendir allows to declaratively state what should be in a directory. It was designed to easily manage libraries for ytt; however, it is a generic tool and does not care how files within managed directories are used.
- [Docs are here](https://carvel.dev/vendir/docs/latest/)