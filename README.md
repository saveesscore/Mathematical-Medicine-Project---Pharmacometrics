The first part of this project is essentially good for creating a reproducible math tool (particularly a function) that takes in five inputs. 
- The current drug mass in the stomach
- The current drug mass in the blood
- How fast it absorbs (ka)
- How fast it clears out (ke)
- Tiny slice of time (dt)

How this helps is that it essentially gives us the ability to look at the human body through a multi-compartment biological model. It treats the stomach and the bloodstream as separate, connected spaces.

In part - the core calculus is just two simple equations. d_stomach represents ds/dt. The drug can only leave the stomach, so its rate of change is entirely negative (-ka * s). d_blood represents db/dt.

The bloodstream is a dynamic system: it is simultaneously gaining drug mass from the stomach (ka * s) and losing drug mass as the kidneys filter it out (-ke *b)

The new_# values predict the future. It takes the current amount of drug and adds the calculated rate of change multipled by a tiny fraction of an hour (dt).

The end of section 1 simply just returns the values and hands them back to the main program, while ensuring concentrations never drop below zero (biologically you can't have a negative amount of chemical in your body).
