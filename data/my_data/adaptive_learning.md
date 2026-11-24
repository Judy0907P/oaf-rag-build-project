# Adaptive learning systems

An adaptive learning system changes what it shows a learner based on how
that learner is performing. Instead of every student getting the same
sequence of lessons, the system estimates what each student already knows
and chooses the next activity to match.

## How adaptation works

Most adaptive systems have three parts:

1. **A content model** that breaks a subject into small skills and records
   which skills depend on which. For example, solving linear equations
   depends on understanding negative numbers.
2. **A learner model** that estimates how well the student knows each
   skill. It is updated after every answer.
3. **A decision rule** that picks the next activity. A common rule is to
   choose a skill the student has not mastered yet but whose prerequisites
   they have mastered.

## Estimating what a student knows

One widely studied technique is Bayesian Knowledge Tracing. It treats
mastery of a skill as a hidden yes-or-no state and updates the probability
of mastery after each answer. It accounts for two kinds of noise: a student
who knows the skill can still slip and answer wrong, and a student who does
not know it can guess correctly.

Another approach comes from Item Response Theory, which models the chance
of a correct answer as a function of the student's ability and the item's
difficulty. It is used heavily in computer-adaptive testing, where harder
questions follow correct answers and easier ones follow mistakes.

## Spaced repetition

Flashcard apps often use spaced repetition: a card you answer correctly is
shown again after a longer gap, and a card you miss comes back soon. This
schedule takes advantage of the spacing effect, the well-replicated finding
that reviewing material spread out over time leads to better long-term
memory than cramming it in one session.

## Limitations

Adaptive systems work best in subjects with clear right answers, such as
arithmetic, vocabulary, or programming syntax. They are harder to build for
essay writing or open-ended problem solving. They also depend on good
content tagging: if skills are mapped incorrectly, the system will
confidently recommend the wrong practice.
