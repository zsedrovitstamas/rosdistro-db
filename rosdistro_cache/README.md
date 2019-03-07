# How to refresh cache:

After you made changes to melodic/distribution.yaml, you will need to refresh this rosdistro_cache in order to be pulled from https://github.com/ms-iot/rosdistro-db/blob/init_windows/index.yaml for public consume. Here is the steps how to do that.

## Prerequisite
You will need to install rosdistro tools.
```
> python -m pip install rosdistro
```

*note*, `rosdistro` should have been installed as part of ROS on Windows. `rosdistro_build_cache` should be able to be found under (ROS) Python\Scripts:
```
>where rosdistro_build_cache
c:\opt\python27amd64\Scripts\rosdistro_build_cache
```
or, check with the `dir` command:
```
>dir c:\opt\python27amd64\Scripts\rosdistro_build_cache
<datetime>             4,334 rosdistro_build_cache
```

## Steps
Here is an example workflow when updating melodic/distribution.yaml

```
> :: clone this repository
> git clone https://github.com/ms-iot/rosdistro-db -b init_windows
> cd rosdistro-db
>
> :: make changes to distribution.yaml
> :: it is important to push the changes so later the rosdistro tool can see the latest changes.
> git add .
> git commit -m "<commit message>"
> git push
>
> :: then, you will need to generate the new cache.
> :: use the path to rosdistro_build_cache found above (c:\opt\python27amd64\Scripts\rosdistro_build_cache)
> cd rosdistro_cache
> python <path to rosdistro_build_cache> https://raw.githubusercontent.com/ms-iot/rosdistro-db/init_windows/index.yaml melodic
>
> :: now check the generated\updated cache files.
> :: for example, melodic-cache.yaml & melodic-cache.yaml.gz will be updated.
> :: if everything looks good, now commit & push it.
> git add .
> git commit -m "refresh cache"
> git push
```
