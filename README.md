# -Transmon-Like-4-Qubit-Lattice-SPSA-Pulse-Daemon-
Floquet-driven 4‑qubit transmon‑inspired lattice simulator that uses SPSA pulse shaping to target ≥0.9996 for the mean transmon-subspace fidelity (proxy) while tracking q‑datagram memory retention and thermodynamic/quantum diagnostics

# Transmon-Inspired Thermodynamic Neuron Dashboard (4-Qubit Lattice)

A research/prototype simulator and visualization dashboard for a **4-qubit (2×2) transmon-inspired lattice**
driven by a **periodic Floquet bath schedule**, with optional **SPSA (GRAPE-ish) pulse shaping** and an optional
**persistent “q-datagram” memory register** (non-Markovian extension).

> ⚠️ This is a **physics-motivated prototype**, not a calibrated transmon device model. Several diagnostics
> (Berry/QGT, “thermodynamic length”, “subspace fidelity”) are implemented as **proxies** for visualization
> and control/optimization.

---

## What it does

- Evolves the **global 4-qubit density matrix (16×16)** under:
  - a coherent Hamiltonian with local terms + couplings (XX+YY, ZZ)
  - local noise channels (dephasing + amplitude down/up) applied as Kraus maps (CPTP by construction)
- Drives the system with a **periodic bath waveform** (square/sine/triangle/sawtooth/gaussian).
- Produces a large “dashboard” animation + metrics:
  - Bloch trajectories, coherence, purity, QFI proxies, Loschmidt echo proxy
  - Bures geometry proxies (Bures angle/length, Bures speed)
  - Lagged-Bures “memory currents”: separation (loss) and return/backflow (gain)
  - Pairwise entanglement: log-negativity + concurrence for all 6 pairs
  - OSEE (operator-space entanglement entropy), MI(01:23)
  - Choi diagnostics for local channels (λ_min, purity)
  - Transmon-ish circuit proxies: ω01(t), EJ/EC, leakage-risk proxy, “subspace fidelity” proxy

    You can paste this section under “CLI Reference”.

Modes & timebase

--mode {single,lattice}

--q_tmax, --dt

Output / rendering

--outdir

FPS controls: --fps, --fps_out, --render_fps, --mp4_fps

Render behavior: --render_skip, --fast_render, --quality {fast,balanced,high,ultra}, --dpi, --viz_scale, --height_boost

TransmonRealDeal

Frames: --render_frames / --no_render_frames, --resume_frames / --no_resume_frames, --keep_frames

Plot data exports: --export_plot_data / --no_export_plot_data, --export_wigner_snapshots

MP4 export: --no_mp4, --mp4_crf, --mp4_preset, --mp4_auto_upsample, --mp4_interp

Wigner (optional visuals)

--no_wigner, --wigner_every, --wigner_N_qubit, --wigner_N_collective, --wigner_smooth_alpha

Drive / transmon‑proxy knobs

--Omega0, --Omega_drive, --target_omega_over_alpha

EC/flux: --transmon_EC, --transmon_flux_amp, --transmon_flux_use_bath / --transmon_flux_no_bath

EJ/EC window clamp: --transmon_EJEC_min, --transmon_EJEC_max, --transmon_EJEC_enforce / --transmon_no_EJEC_enforce

Leakage guard:
--transmon_leak_guard / --transmon_no_leak_guard,
--transmon_fid_floor, --transmon_leak_guard_scale, --transmon_drive_headroom,
--transmon_leak_kappa, --transmon_leak_guard_mode {soft,hard}

Bath schedule / thermal pulses

Enable/disable: --bath_enable / --bath_disable

Shape/period: --bath_waveform {square,sine,triangle,sawtooth,gaussian}, --bath_period, --bath_duty

Phase: --bath_global_phase, --bath_phase_per_qubit

Mod depth: --bath_amp_gamma, --bath_amp_drive, plus overall scales --bath_gamma_scale, --bath_drive_scale

Temperature endpoints: --T_bath_base_mK, --T_bath_hot_mK

q‑datagram quantum memory register

--qmem_enable

--qmem_nmem, --qmem_theta_in, --qmem_theta_out

--qmem_inject_every, --qmem_update_every, --qmem_mem_init {zero,maxmix}

Couplings + entanglement pump

--J_cap, --J_ind

--ent_boost, --ent_pulse_amp

Hotspots/leak view: --hotspot_thr, --leak_warn, --leak_warn_frac, --leak_plot_mode, --leak_plot_scale

Choi traces: --choi_per_qubit

Disable overlays: --no_hotspot_trails, --no_hotspot_flares, --no_hotspot_tl

--ent_tests (unit tests then exit)

Daemon optimization

--daemon, --daemon_iters, --daemon_pulses, --daemon_seed

Sharing (optional)

--ngrok / --enable_ngrok, --ngrok_authtoken / --ngrok_token, --ngrok_port

---

## Install

### Minimal
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
1.) Lipka-Bartosik, P., Perarnau-Llobet, M., & Brunner, N. (2024). Thermodynamic computing via autonomous quantum thermal machines. Sci. Adv. 10, eadm8792.
