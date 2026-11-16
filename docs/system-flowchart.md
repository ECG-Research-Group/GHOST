# GHOST system flowchart

GHOST lifts fish tails and records the force during each lift to support monitoring of rigor mortis progression across time and treatments. The motion and measurement chain below applies to each of the four channels.

```mermaid
flowchart TD
    subgraph E[Electronics box]
        PI[Raspberry Pi 4]
        MC[Motor-control boards]
        P12[12 V PSU]
        P24[24 V PSU]
        PI -->|Motion commands| MC
        P12 -.->|Motor power| MC
    end

    subgraph G[GHOST stand - four channels]
        MOTOR[Stepper motors drive linear actuators]
        LIFT[Hooks lift fish tails]
        CELL[Load cells sense lifting force]
        AMP[Load-cell amplifiers condition the signals]
        MOTOR --> LIFT --> CELL
        CELL -->|Load-cell signals| AMP
    end

    MC -->|Controlled motor drive| MOTOR
    P24 -.->|24 V amplifier power| AMP
    AMP -->|Amplified analog outputs| PL[PowerLab - four-channel data acquisition]
    PL -->|Measurement data| LC[LabChart on laptop]
    LC --> SAVE[Observe, annotate and store measurements]
    SAVE --> COMPARE[Compare measurements across lifts and treatments]
    COMPARE --> RESULT[Interpret rigor mortis progression using the study protocol]

    classDef power fill:#fff0dc,stroke:#ed7900,color:#172b4d
    classDef motion fill:#e8f2ff,stroke:#087bea,color:#172b4d
    classDef signal fill:#e9f8eb,stroke:#199539,color:#172b4d
    classDef data fill:#f4eaff,stroke:#8125ba,color:#172b4d
    class P12,P24 power
    class PI,MC,MOTOR,LIFT motion
    class CELL,AMP signal
    class PL,LC,SAVE,COMPARE,RESULT data
```

The intended lift interval is one hour. Exact motion settings and synchronization between actuator motion and acquisition remain undocumented. Power-supply arrows show power delivery; they do not indicate software control or measurement feedback.
