# Honesty Rules

What public copy in any of the four repos may claim. Stage 05 audits every public page
against this list. The rule underneath all of them is Flight Eye's: never show a number
nobody measured.

## Always

1. **Say "simulation" next to every simulated number, track or log.** Contract C6 in
   `integration.md` says what the block contains.
2. **Name the simulator.** "Python sim" and "ArduPilot SITL" are different claims. The Python
   sim is a kinematic model written in this repo; SITL is the real flight code on a desktop.
3. **Show "not measured" for a value nobody read.** Never zero, never "nominal", never blank.
4. **Date-stamp prices, versions and regulations**, and cite the URL.
5. **Keep "in progress" and "simulation only" wherever the drone project is described.**
   The cover letter already says this. Every page has to agree with it.

## Never

1. "Operated", "flew", "piloted" or "deployed" for anything that ran only in simulation.
   Use "ran in simulation", "rehearsed", "simulated".
2. An employer's name, logo, product names or colours on any public page.
3. A metric that came from a hand-edited log. Logs shown publicly come from a scenario run,
   are committed unedited, and pass `verify-log`.
4. "Secure", "tamper-proof" or "military grade" for the ops log, the consent gate or the
   accounts. The log is tamper-evident; consent is a speed bump; passkeys resist phishing.
   Those are the claims.
5. A lessons-learned paragraph the generator wrote. The generator fills findings from the
   log; lessons are written by a person, and the section says "not yet written" until one is.

## Wording Bank

| Instead of | Write |
|-----------|-------|
| "Autonomous drone" | "ArduPilot quadcopter, scripted from a ground PC, in simulation so far" |
| "USV operations experience" | "Surface vessel missions rehearsed in ArduPilot Rover simulation" |
| "Detected and handled the failure" | "The monitor flagged it in N s; the simulated flight controller's failsafe returned it to launch" |
| "Secure log" | "Tamper-evident log: altering a line breaks the chain, and `verify-log` says which line" |
