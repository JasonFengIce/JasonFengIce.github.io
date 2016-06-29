---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-06-21 14:22:57 +0800
categories: jekyll update
---

{% highlight java %}
    private void timerCountDown() {
        Observable<Integer> observable = countdown(5);
        observable.doOnSubscribe(new Action0() {
            @Override
            public void call() {
                Log.i(TAG, "开始计时");
            }
        }).subscribe(new Subscriber<Integer>() {
            @Override
            public void onCompleted() {
                Log.i(TAG, "计时完成");
                intentToLauncher();
            }

            @Override
            public void onError(Throwable e) {
                Log.e(TAG, "计时出错: " + e.getMessage());
            }

            @Override
            public void onNext(Integer integer) {
                Log.i(TAG, "当前计时：" + integer);
                timerText.setImageResource(secondsResId[integer - 1]);
            }
        });
    }
{% endhighlight %}

{% highlight java %}
    public Observable<Integer> countdown(int time) {
        if (time < 0) time = 0;

        final int countTime = time;
        return Observable.interval(0, 1, TimeUnit.SECONDS)
                .subscribeOn(AndroidSchedulers.mainThread())
                .observeOn(AndroidSchedulers.mainThread())
                .map(new Func1<Long, Integer>() {
                    @Override
                    public Integer call(Long increaseTime) {
                        return countTime - increaseTime.intValue();
                    }
                })
                .take(countTime);
    }
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
