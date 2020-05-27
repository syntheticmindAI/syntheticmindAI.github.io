---
layout: post
title: TRAINING GAME AGENTS WITH SUPERVISED LEARNING
date: 2020-01-29 01:00 +0700
modified: 2020-03-07 16:49:47 +07:00
description: Ada dua cara untuk memperbarui forked repository menggunakan web interface yang disediakan oleh github tapi ribet, atau melalui terminal yang lebih ribet lagi.
tag:
  - tips
  - git
  - software
image: /cara-memperbarui-fork-repository/repo.png
---

Reinforcement Learning is a general, robust and performant paradigm. Its strengths become evident when combined with deep learning. Deep reinforcement learning can solve increasingly complex tasks with huge state space and complex rules. It has produced world champion-beating artificial agents in the games of chess, DOTA, go, and Starcraft. One may argue that any problem where scores are received for performing actions should be framed as a reinforcement learning problem. But behind these notable successes, lies huge problems. Deep reinforcement learning is hard to work with. A lot of effort goes into making agents learn correctly and robustly. Deep reinforcement learning also needs a huge amount of compute. Hundreds of thousands of dollars in compute is needed to reproduce the most impressive results. A lone researcher with limited resources cannot comfortably go beyond Atari games state space when experimenting with game playing agents. 

Lots of effort has been made to improve the sample efficiency of these deep RL algorithms. Model based reinforcement learning is a promising research direction. The environment dynamics can be mastered using supervised/ self-supervised learning, then smaller representations can be used to learn to maximise cumulative reward. This paradigm is attractive because once you learn representations of the state, you may use any kind of valid algorithm to maximise rewards.

Another promising paradigm is Upside down RL, where the appropriate action to take in a given state is learned by injecting additional information when learning to map state to actions. In settings where this has worked,  an expected goal, in addition to the state, is used as input. The agent is trained to produce actions that reach the goal. The goal in this case is to gain a given reward in a given number of time steps. Inspiration from this paradigm leads me to this month's article.

We know that we can use a neural network to map state to actions and use a reward proxy in our loss function to maximise the probability that the actions taken will yield the highest reward. 
An example of this loss function is the policy gradient loss:


<figure>
<img src="{{ page.image }}" alt="ilustrasi repo yang mau diupdate">
<figcaption>Fig 1. Gambaran ribetnya.</figcaption>
</figure>

Ada dua cara untuk memperbarui forked repository menggunakan web interface yang disediakan oleh github tapi ribet, atau melalui terminal yang lebih ribet lagi.

### Melalui Github (boring way) 💻

1. Buka repo yang hasil fork di Github.
1. Klik **Pull Requests** di sebelah kanan, lalu **New Pull Request**.
1. Akan memunculkan hasil compare antara repo upstream dengan repo kamu(forked repo), dan jika menyatakan "There isn’t anything to compare.", tekan link **switching the base**, yang mana sekarang repo kamu(forked repo) akan dibalik menjadi base repo dan repo upstream menjadi head repo.
1. Tekan **Create Pull Request**, beri judul pull request, Tekan **Send Pull Request**.
1. Tekan **Merge Pull Request** dan **Confirm Merge**.

\* _pastikan kamu tidak merubah apapun pada forked repo, supaya melakukan merge secara otomatis, kalo tidak ya paling2 konflik._

### Melalui terminal ⌨️

Tambahkan remote alamat repository yang aslinya disini tak beri nama `upstream`., ganti `ORIGINAL_OWNER` dan `ORIGINAL_REPO` dengan alamat repo aslimu.

```bash
$ git add remote upstream git@github.com:ORIGINAL_OWNER/ORIGINAL_REPO.git
$ git remote -v
> origin    git@github.com:piharpi/www.git (fetch) # forked repo
> origin    git@github.com:piharpi/www.git (push) # forked repo
> upstream    git@github.com:ORIGINAL_OWNER/ORIGINAL_REPO.git (fetch) # upstream repo / original repo
> upstream    git@github.com:ORIGINAL_OWNER/ORIGINAL_REPO.git (push) # upstream repo / original repo
```

Checkout ke local branch `master`.

```bash
$ git checkout master
> Switched to branch 'master'
```

Jika sudah, Merge local repo dengan remote `upstream/master`.

```bash
$ git merge upstream/master
```

Terakhir push local repo ke remote `origin`.

```bash
$ git add -A
$ git commit -m "updating origin repo" && git push -u origin master
```

Selamat mencoba cara ribet ini, semoga bisa dipahami, saya sendiri lebih senang melalui terminal, klo ada yang ribet kenapa cari yang mudah.

##### Resources

- [Syncing a fork](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)
- [Update your fork directly on Github](https://rick.cogley.info/post/update-your-forked-repository-directly-on-github/#top)
