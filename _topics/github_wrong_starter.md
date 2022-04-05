---
topic: "github: wrong starter"
desc: "help! I pulled from the wrong starter"
indent: true
category_prefix: "github:"
---


# Help! I pulled from the wrong starter

Here is an example of what it might look like if you pulled from the wrong starter repo, and *how to fix it*.

# First, the part that's correct

Here, we clone a `jpa01-fakeStudent` repo, and we see that the `origin` remote is correct:

```
pconrad@Phillips-MacBook-Pro ucsb-cs156-s22 % git clone git@github.com:ucsb-cs156-s22/jpa01-fakeStudent.git
Cloning into 'jpa01-fakeStudent'...
warning: You appear to have cloned an empty repository.
pconrad@Phillips-MacBook-Pro ucsb-cs156-s22 % cd jpa01-fakeStudent 
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % git remote -v
origin	git@github.com:ucsb-cs156-s22/jpa01-fakeStudent.git (fetch)
origin	git@github.com:ucsb-cs156-s22/jpa01-fakeStudent.git (push)
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % 
```

# Now, we set up the wrong starter

We intended to set up STARTER-jpa01 as our starter, but instead we set up STARTER-jpa00:

```
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % git remote add starter git@github.com:ucsb-cs156-s22/STARTER-jpa00.git    
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % git remote -v
origin	git@github.com:ucsb-cs156-s22/jpa01-fakeStudent.git (fetch)
origin	git@github.com:ucsb-cs156-s22/jpa01-fakeStudent.git (push)
starter	git@github.com:ucsb-cs156-s22/STARTER-jpa00.git (fetch)
starter	git@github.com:ucsb-cs156-s22/STARTER-jpa00.git (push)
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % 
```

Ouch!   `starter` refers to `git@github.com:ucsb-cs156-s22/STARTER-jpa00.git ` when we intended `git@github.com:ucsb-cs156-s22/STARTER-jpa01.git`

We can see that when we type `git remote -v`

# Doubling down

Now suppose we double down on the error and populate the repo with the wrong code

```
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % git checkout -b main
Switched to a new branch 'main'
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % git pull starter main
remote: Enumerating objects: 39, done.
remote: Counting objects: 100% (39/39), done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 39 (delta 14), reused 39 (delta 14), pack-reused 0
Unpacking objects: 100% (39/39), 7.81 KiB | 420.00 KiB/s, done.
From github.com:ucsb-cs156-s22/STARTER-jpa00
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> starter/main
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % git push origin main
Enumerating objects: 39, done.
Counting objects: 100% (39/39), done.
Delta compression using up to 16 threads
Compressing objects: 100% (32/32), done.
Writing objects: 100% (39/39), 7.83 KiB | 2.61 MiB/s, done.
Total 39 (delta 14), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (14/14), done.
To github.com:ucsb-cs156-s22/jpa01-fakeStudent.git
 * [new branch]      main -> main
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % ls
LICENSE		README.md	pom.xml		src
pconrad@Phillips-MacBook-Pro jpa01-fakeStudent % 
```

Now, the wrong code is in our repo.  What to do!?!?  Should we just delete the repo and start over?!!

We could.  But there's a better way.

# Fixing it

The first step in fixing it is to remove the old remote and redefine it as the correct one:

