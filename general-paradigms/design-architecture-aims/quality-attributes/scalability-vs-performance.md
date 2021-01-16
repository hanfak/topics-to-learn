# Scalability vs performance

- Both are linked
- if the performance of a software system deteriorates rapidly with increasing load (number of users or volume of transactions) prior to reaching the intended load level, then it is not scalable and will eventually underperform
  - The aim is to have the performance of a software system would sustain as a flat curve with increasing load prior to reaching the intended load level
  - classified as type I scalability issue, can be overcome with proper optimizations and tunings
- If the performance of a software system becomes unacceptable when reaching a certain load level with a given environment, but it cannot be improved even with upgraded and/or additional hardware, then it is said that the software is not scalable.
  -  type II scalability issue, cannot be overcome without going through some major architectural operations, which should be avoided from the beginning at any cost.
- What performance a software system exhibits often solely depends on the raw speed of the underlying hardware platform, which is largely determined by the central processing unit (CPU) horsepower of a computer.
- What scalability a software system exhibits depends on the scalability of the architecture of the underlying hardware platform 
