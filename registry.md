## Working with private registry

##### List all images with tags. [JQ package](https://stedolan.github.io/jq/) is required

```bash
registry_url="https://user:password@some.repo.com"

repos=$(curl --silent ${registry_url}/v2/_catalog) | jq --raw-output ".repositories"

for repo in $(echo "${repos}" | jq -r '.[]'); do
    # echo ${repo}
    tags=$(curl --silent ${registry_url}/v2/${repo}/tags/list | jq  --raw-output ".tags")
    for tag in $(echo "${tags}" | jq -r '.[]'); do
        echo "${repo}:${tag}"
    done
done

```