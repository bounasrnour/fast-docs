# GANs

## what are Gans?

consists of 2 networks playing adversary 

- the GENERATOR
- the DISCRIMINATOR

example the generator tries to make a fake 100$ bill 
the discriminator compare the fake 100$ bill to the real one and then he says that the one comming from the generator is fake , the generator was not able to fool the discriminator
as training the generator becomes better and will be able to fool the discriminator
at the end the generator creates an indistinguishable 100$ bill from the real one and the discriminator foced to guess with probability 1/2

**note**   both discriminator and generator starts from scratch

## Loss function

Discriminator loss function : $\frac{1}{m}\ \sum ^m [logD(x^i )+ log(1 - D(G(z^i)))]$

D : discriminator
G : generator
z : random noise
the discriminator tries to maximise this expression 
the generator wants to minimize this expression 