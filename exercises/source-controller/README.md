# Source controller
The main component of Flux is the source controller. It's main role is to download artifacts from external sources like Git repositories, Helm repositories or S3 buckets. It will handle authentication, detect source changes and fetch sources on-demand or on-a-schedule. The artifacts will be packaged into a well-known format and can be used by other Flux components like the helm-controller.

## Exercises
1. Set the FLUX_SYSTEM_NAMESPACE environment variable. By default flux cli will use flux-system. It is also possible to add -n \<NAMESPACE> to all you commands.
```
export FLUX_SYSTEM_NAMESPACE=<NAMESPACE>
```
2. Create a Flux Gitrepository source with SSH by using the following command.
```
flux create source git flux-fundamentals \
    --url=https://github.com/jeroensmit/gitops-fundamentals-exercises \
    --username=jeroensmit \
    --password=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 \
    --branch=main \
    --interval=10m
```

> REPO_URL example > --url=https://github.com/guidalabs/gitops-fundamentals-exercises.git

3. Your source should now be added. Verify that the git source is added correctly by running:
```
flux get source git flux-fundamentals
```
4. Export this Git Source as a yaml file.
```
flux export source git flux-fundamentals > cluster/staging/flux-source.yaml
```
5. Figure out a way to create a flux Helm source from the public helm repository podinfo (https://stefanprodan.github.io/podinfo)

6. Confirm that your Helm source is ready and export this as a yaml file as well.
```
flux export source helm podinfo > repositories/podinfo.yaml
```
7. Push these changes to Git.
8. Your Git repository will be synced every 10 minutes, but you can also manually reconcile your repository by running:
```
flux reconcile source git flux-fundamentals
```
9. Confirm that the fetched revision matches your latest git commit.
