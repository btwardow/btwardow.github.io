---
layout: post
title:  "Using matrix factorization in recommendation"
date:   2014-09-22 21:08:42
categories: data_science reco
---

Scala and Breeze
===

Simple matrix factorization function using gradient decent method:

{% highlight scala linenos %}
  def matrixFactorization(r:DenseMatrix[Double], xInit:DenseMatrix[Double], yInit:DenseMatrix[Double], k:Int, steps:Int = 5000, alpha:Double = 0.0002, beta:Double = 0.02, errorThreshold:Double = 0.001): (DenseMatrix[Double], DenseMatrix[Double]) = {

    var e = Double.MaxValue
    var x = xInit
    var y = yInit.t

    for( step <- 1 to steps if e > errorThreshold) {

      //update matrix
      r.findAll( _ > 0 ).foreach{ case (i,j) => {

        val eij = r(i, j) - (x(i, ::) * y(::, j))

        //gradient
        for (k_ <- 0 until k) {
          x(i, k_) += alpha * ((2 * eij * y(k_, j)) - (beta * x(i, k_)))
          y(k_, j) += alpha * ((2 * eij * x(i, k_)) - (beta * y(k_, j)))
        }

      }}

      //calculate error
      e=0

      r.findAll(_ > 0).foreach { case (i, j) => {
        val eij = r(i, j) - (x(i, ::) * y(::, j))
        e += pow((r(i, j) - eij), 2)
        for (k_ <- 0 until k) {
          e += (beta / 2) * (pow(x(i, k_), 2) + pow(y(k_, j), 2))
        }
      }}

    }

    (x,y)
  }
{% endhighlight %}


{% gist 9cb461c0c1aed6c6e797 %}

