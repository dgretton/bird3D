# Bird for BirdOS

**Intuitive 3D pointing based on hand tracking for VR, AR, CAD, drone piloting, volumetric data navigation and other settings for 3D user interfaces**

*Aubrey Simonson and Dana Gretton*

## Introduction

Bird is a hand-controlled pointing system that translates a user's finger movements and positions into the motion of a 3D pointer in a virtual space, which allows a smooth control of a 3D graphical user interface (GUI). Bird was first conceived by Aubrey Simonson (MIT Media Lab Object Based Media Group) and elaborated during subsequent conversations with Dana Gretton (MIT Media Lab Sculpting Evolution Group) in 2017-2018. The name Bird stems from its similarity to a computer mouse, named for an animal occupying the ground, evolved with the addition of a third degree of freedom into an animal occupying the air. The first demonstration of Bird was in April 2019, when it was used as part of a working 3D virtual reality interface to move 3D objects about in a scene. The prototype system and application, jointly developed by Aubrey and Dana, was originally wired to a computer, utilizing bend-sensitive resistors and a microcontroller to sense finger motion. A commercial VR system was used to track gross hand position. Later versions are envisioned as wireless devices, possibly not hand-mounted at all. Bird is not a particular device, but rather a framework and paradigm for translating hand and finger motion into precise, intuitive 3D positioning that is 1) not limited in virtual space by arm reach; 2) capable of precisely specifying range as well as direction; 3) amenable to adaptation of existing abstractions in 2D, mouse-centered GUIs; 4) easy to learn; 5) usable in many different postures and resistent to fatigue; and 6) transendent of the limitations of literal hand position tracking.

## Principle of operation

The basic principle of Bird is to treat finger extension (the degree to which a finger is more uncurled and straight) as an intention, in an absract sense, for the bird pointer to move away from the hand. Extension values for all fingers on one hand, including the thumb, are monitored very precisely in real time. As with a 2D computer mouse, the pointer finger is reserved for selecting and activating user interface (UI) elements, and its extension is ignored for tracking. Hand orientation at the wrist loosely dictates the direction of the path along which the bird should move as the fingers extend. When all of the fingers are extended fully, creating a plane with the palm, the bird is at maximum range from the user. In a fist, the bird is at minimum range, in which case its position might correspond well with the actual position of the user's hand in real space. In between, the position of the bird is calculated as a smooth transformation of the four finger extension values (middle, ring, pinky, thumb) such that fine, independent adjustments of the fingers can be used to fine-tune the position of the bird. Some degree of de-noising and inference is performed to remove hand vibrations and noise to the greatest extent possible without compromising responsiveness.

Within this framework, many specific programmatic implementations are possible. One way to formalize the particular smooth transformation is to use the finger extension values to calculate a best-fit sphere to the hand and palm, and take the center of this sphere as the bird position. Thus, when the hand is mostly closed as if to hold a kiwi-sized object, the bird is just a few centimeters off of the palm; when the hand is shaped more as if to hold a large melon, the bird might be at a range of ten or more centimeters from the palm; and when the hand is mostly flat, the bird recedes to an arbitrary distance from the palm, maybe hundreds of meters or kilometers. Another way to formalize the smooth transformation is to add up the extension values for all of the fingers and use that sum, scaled by an appropriate constant, as an offset from the hand along a ray approximately out of the palm. Both of these implementations allow small adjustments of finger position to change the distance of the bird from the hand in a predictable way. In either case, the hand orientation as controlled by the wrist and forearm is the dominant influence on "where" the bird is apparently pointing, and the range as a function of finger position is the main difference. Each of these approaches has strengths and weaknesses, and our point is that there is no particular correct solution; the best smooth map will surely be something in between, and will emerge with continued prototyping and iteration. It is expected that even if a user becomes accustomed to one smooth map, they will likely adapt quickly to a new smooth map, just as they might adapt after switching between mouse sensitivities on a desktop.

## Features

This scheme for 3D pointing is attractive for several reasons. It is intuitive, in that if the user wishes to interact with something far away outside their arms' reach, they can reach out with an open hand and arrive at it after some adjustment, and if the user wants to interact with something close at hand, they can access it by grabbing at it. By offering access to UI elements at both close and far range, Bird can take advantage of the fact that the virtual world synthesized for the user is infinite in extent, opening up modes of interaction far beyond what is possible using UI elements that can be accessed within physical reach. We imagine a mode whereby the user waves their bird across many meters of space over to a target object representing an application, uses their pointer finger to select it to move it, closes their hand to bring it close, and activates a Bird-integrated trigger to open it.

