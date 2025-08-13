# Unidad 2


## 🛠 Fase: Apply

stateDiagram-v2
    [*] --> CONFIG : boot / T_conf=20; mostrar(T_conf)
    state CONFIG {
        [*] --> AJUSTE
        AJUSTE --> AJUSTE : UP [T_conf<60] / T_conf+=1; beep(); mostrar(T_conf)
        AJUSTE --> AJUSTE : DOWN [T_conf>10] / T_conf-=1; beep(); mostrar(T_conf)
    }
    CONFIG --> COUNTDOWN : ARMED (shake) / t_ms=T_conf*1000; start_ms=ticks_ms(); mostrar_secs(t_ms)
    CONFIG --> CONFIG : TOUCH / feedback()  %% sin cambio; opcional reset visual

    state COUNTDOWN {
        [*] --> TICK
        TICK --> TICK : tick (Δt) / t_ms-=Δt; mostrar_secs(t_ms)
    }
    COUNTDOWN --> EXPLODED : [t_ms<=0] / explosionFX(); mostrar("X")
    COUNTDOWN --> CONFIG : TOUCH / stop_sounds(); mostrar(T_conf)

    EXPLODED --> CONFIG : TOUCH / stop_sounds(); mostrar(T_conf)
