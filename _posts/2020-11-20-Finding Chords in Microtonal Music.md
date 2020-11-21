---
author: Lawrence Borst
excerpt_separator: <!--more-->
permalink: microtonal
description: categorization of consonant microtonal chords
tags: [music, microtonal music, chords]
layout: post
---
I see microtonal music as an often dissonant art. This perception owes itself in part to its strangeness, but also to scientific principles that make many types of microtonal music unattractive to the uninitiated. For example, imagine a pitch. Play it in your head, and then layer it with a second pitch just slightly above the first. What you're hearing is a dissonant interval, and we shall go over the reason why that may be. We will attempt to categorize chords by their "pleasantness" to the ear, and show how this problem can be handled mathematically.

But before we can dive into microtonality we need to understand Western tuning, how sound is perceived, and what makes a sound pleasant.

<!--more-->

<h2>The Octave, Pitches and Sound Waves</h2>

A good starting point is the octave. The octave is an interval, meaning it denotes a pitch relationship between two notes. The octave is a natural starting point when it comes to tuning. When I play a C4 and a C5 simultaneously on a piano, it will sound harmonious. Perfect. In fact, the C4 and C5 "feel" similar, and musicians may use terms like "perfect octave" to describe such assonant intervals. You could say C5 sounds like a "higher" C4. But when we shift somewhere arbitrary, like E5, we would not say it sounds like a "higher" C4... But we could say it sounds like a higher E4-if you're human, that is.

A pitch in music is a perceptual property of sound. A sound is a pressure wave, and for a pitched sound, the pressure it carries to your ear will be periodic. A sound wave can be quite arbitrary; pitch will be perceived as long as it is periodic. Your brain is able to distinguish the frequency of sound, and from this frequency perceives a pitch. While we'll talk a lot about "pitch", I remind the reader that pitch is only a perception, and the frequency of sound waves is fundamentally where music happens physically.

So what makes the octave special? It is this: if the "lower" sound has pitch $x$, then the "higher" sound will have pitch $2x$. Precisely $2x$. If we begin to deviate, by playing at say a frequency of $2x+\epsilon$, the resulting interval will sound less harmonious.

I don't think we fundamentally know <b>why</b> our brains favor intervals such as this—in fact, it isn't even clear if animals have opinions about intervals at all—but it seems to be the way it works. We can, however, make a guess why the two pitches sound "similar". Maybe it is because a sound with frequency $2x$ necessarily also has frequency $x$. This does, however, not reveal why the magic number is $2$, instead of $3$ or something. (But the brain <b>does</b> favor sounds at frequencies $x$ and $3x$ played simultaneously. This would be a perfect twelfth, and sounds harmonious, but nothing like duplicating a sound)

<h2>Equal Temperament Tuning</h2>

We shall briefly look at the Western tuning system, because microtonality naturally extends it. Western tuning—in particular what we might call equal temperament—can be constructed from two pieces of information: a reference pitch, and the number of equal intervals we split an octave into. The reference pitch acts like an "origin", and in Western music we could set it at A4, which we define to be $440$Hz (ocillations/repetitions per second of a sound).

So what should A5 be, one octave up? Well, $880$Hz, from the previous discussion. A6? Perhaps it is tempting to bet on $1320=3(440)$, but it is 1760Hz, because the relationship between A6 and A5 is the same between A5 and A4. That is, A6 doubles the frequency associated with A5, the same way A5 doubles that with A4.

The reader may recognize that when we choose to split the octave into equal intervals, we are forced not to cut the octave into equal frequencies, but rather to pick frequencies in geometric progression. This multiplicative behavior may seem striking, but in a way pitch perception is not much different from how humans perceive many other stimuli (see Steven's power law). Loudness, touch sensitivity, pitch and warmth perception all follow power laws with respect to our "perceived intensity". In a sense, pitch and vibrations are related by Steven's power law. But I digress.

So if we start with A4 at $440$Hz, what frequency should the next note (Bb4) be? Well, say we wish to split A4 to A5 into twelve equal intervals, and each interval takes us further by a (multiplicative) factor of x. Then, moving up 12 steps (semitones), we get $440x^{12}=880$, giving $x=\sqrt[12]{2}$. Then Bb4 is at $440\sqrt[12]{2}\approx 466.16$.

At this point we can construct all $88$ keys on the keyboard with their associated frequencies. We'll leave tuning at that for now, though the subject goes much deeper in practice—there are infinite families of tuning systems to draw from! The tuning system here is most commonly used on synthesizers, electric guitars, and keyboard instruments, just to name a few.

<h2>The Mathematics of Consonant Intervals: Basic Limit Theory</h2>

We're nearing the prerequisite knowledge to understand how to tackle microtonality. But to solve the problem of finding pleasant chords in it, we need to understand "consonance" and "dissonance".

Where "consonance" conveys something pleasant, "dissonance" conveys something unnerving. This is the same to how "consonance" and "dissonance" are used to talk about intervals. The mathematical machinery of consonant intervals is every bit as harmonious as its sound.

Roughly, when two notes $A$ and $B$ are heard, the "closer" the ratio between their associated frequencies $f(A):f(B)$ is to a rational number of the form $a:b$ with small $a$ and $b$ (coprime), the more harmonious it sounds.

For example, $f(A5):f(A4)=2:1$ is very harmonious. This is an the pitch ratio associated with an octave. For a perfect fifth, which is considered the "second-most" consonant interval, we have something like $f(A5):f(E5)=\sqrt[12]{2^{7}}\approx 1.498$ because a perfect fifth has 7 "steps" (semitones). This number is irrational, and so you may expect it to be very dissonant. But it is also awfully close to a "nice rational number", namely $3:2=1.5$ That is why it sounds "nice".

But how do we characterize "closeness?"