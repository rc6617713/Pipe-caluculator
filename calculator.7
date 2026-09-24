import math
import streamlit as st

# =========================================================
# PAGE CONFIGURATION
# =========================================================
st.set_page_config(
    page_title="Pipe Flow Calculator",
    page_icon="🚰",
    layout="wide"
)

# Gravitational acceleration
g = 9.81


# =========================================================
# CORE FORMULATION FUNCTIONS
# =========================================================

def reynolds_number(rho, velocity, diameter, viscosity):
    if viscosity <= 0:
        return 0
    return (rho * velocity * diameter) / viscosity


def kinematic_viscosity(viscosity, rho):
    if rho <= 0:
        return 0
    return viscosity / rho


def reynolds_using_kinematic(velocity, diameter, nu):
    if nu <= 0:
        return 0
    return (velocity * diameter) / nu


def relative_roughness(roughness, diameter):
    if diameter <= 0:
        return 0
    return roughness / diameter


def laminar_friction_factor(Re):
    if Re <= 0:
        return 0
    return 64 / Re


def turbulent_friction_factor(Re, roughness, diameter):
    if Re <= 0 or diameter <= 0:
        return 0.02

    f = 0.02  # Initial guess
    for _ in range(100):
        old_f = f
        try:
            term = (roughness / (3.7 * diameter)) + (2.51 / (Re * math.sqrt(f)))
            f = 1 / (-2 * math.log10(term)) ** 2
        except (ValueError, ZeroDivisionError):
            break

        if abs(f - old_f) < 1e-8:
            break
    return f


def friction_factor(Re, roughness, diameter):
    if Re <= 0:
        return 0.0
    if Re < 2300:
        return laminar_friction_factor(Re)
    else:
        return turbulent_friction_factor(Re, roughness, diameter)


def head_loss(f, length, diameter, velocity):
    if diameter <= 0:
        return 0.0
    return f * (length / diameter) * ((velocity ** 2) / (2 * g))


def pressure_drop(rho, hf):
    return rho * g * hf


def direct_pressure_drop(f, rho, length, diameter, velocity):
    if diameter <= 0:
        return 0.0
    return f * (length / diameter) * ((rho * (velocity ** 2)) / 2)


def pascal_to_kpa(pressure_pa):
    return pressure_pa / 1000.0


def flow_regime(Re):
    if Re <= 0:
        return "Invalid / No Flow"
    elif Re < 2300:
        return "Laminar"
    elif Re <= 4000:
        return "Transitional"
    else:
        return "Turbulent"


# =========================================================
# STREAMLIT USER INTERFACE
# =========================================================

st.title("🚰 Pipe Flow & Fluid Mechanics Calculator")
st.markdown("Calculate fluid behavior, flow regimes, friction factors, and pressure losses in circular pipes.")

# Visual Tabs replacing CLI menu
tab_all, tab_re, tab_f, tab_hf, tab_dp = st.tabs([
    "⚡ Comprehensive Analysis (All)",
    "📊 Reynolds Number",
    "🌀 Friction Factor",
    "📏 Head Loss",
    "💥 Pressure Drop"
])


# ---------------------------------------------------------
# TAB 1: COMPREHENSIVE ANALYSIS
# ---------------------------------------------------------
with tab_all:
    st.header("Full System Calculation")
    
    col1, col2 = st.columns(2)
    
    with col1:
        st.subheader("Fluid Properties")
        rho = st.number_input("Density, ρ (kg/m³)", value=1000.0, step=10.0, key="all_rho")
        viscosity = st.number_input("Dynamic Viscosity, μ (Pa·s)", value=0.001002, format="%.6f", key="all_visc")
        
    with col2:
        st.subheader("Pipe & Flow Parameters")
        diameter = st.number_input("Pipe Diameter, D (m)", value=0.05, format="%.4f", key="all_d")
        length = st.number_input("Pipe Length, L (m)", value=10.0, step=1.0, key="all_l")
        velocity = st.number_input("Fluid Velocity, V (m/s)", value=2.0, step=0.1, key="all_v")
        roughness = st.number_input("Pipe Roughness, ε (m)", value=0.000045, format="%.6f", key="all_e")

    if st.button("Run Full Calculation", type="primary", use_container_width=True):
        Re = reynolds_number(rho, velocity, diameter, viscosity)
        nu = kinematic_viscosity(viscosity, rho)
        Re_check = reynolds_using_kinematic(velocity, diameter, nu)
        regime = flow_regime(Re)
        rr = relative_roughness(roughness, diameter)
        f = friction_factor(Re, roughness, diameter)
        hf = head_loss(f, length, diameter, velocity)
        delta_p = pressure_drop(rho, hf)
        direct_dp = direct_pressure_drop(f, rho, length, diameter, velocity)
        delta_p_kpa = pascal_to_kpa(delta_p)

        st.divider()
        st.subheader("Results")

        m1, m2, m3 = st.columns(3)
        m1.metric("Reynolds Number (Re)", f"{Re:,.2f}")
        m2.metric("Flow Regime", regime)
        m3.metric("Friction Factor (f)", f"{f:.6f}")

        m4, m5, m6 = st.columns(3)
        m4.metric("Kinematic Viscosity (ν)", f"{nu:.8f} m²/s")
        m5.metric("Relative Roughness (ε/D)", f"{rr:.6f}")
        m6.metric("Head Loss (h_f)", f"{hf:.4f} m")

        st.divider()
        res_col1, res_col2 = st.columns(2)
        res_col1.metric("Pressure Drop (Hydrostatic)", f"{delta_p:.2f} Pa", f"{delta_p_kpa:.4f} kPa")
        res_col2.metric("Direct Pressure Drop", f"{direct_dp:.2f} Pa")


# ---------------------------------------------------------
# TAB 2: REYNOLDS NUMBER ONLY
# ---------------------------------------------------------
with tab_re:
    st.header("Calculate Reynolds Number & Regime")
    
    c1, c2 = st.columns(2)
    rho_re = c1.number_input("Density (kg/m³)", value=1000.0, key="re_rho")
    v_re = c2.number_input("Velocity (m/s)", value=2.0, key="re_v")
    d_re = c1.number_input("Diameter (m)", value=0.05, format="%.4f", key="re_d")
    mu_re = c2.number_input("Dynamic Viscosity (Pa·s)", value=0.001002, format="%.6f", key="re_mu")

    if st.button("Calculate Reynolds Number", use_container_width=True):
        Re_val = reynolds_number(rho_re, v_re, d_re, mu_re)
        reg_val = flow_regime(Re_val)
        
        st.success(f"**Reynolds Number:** {Re_val:,.2f}")
        st.info(f"**Flow Regime:** {reg_val}")


# ---------------------------------------------------------
# TAB 3: FRICTION FACTOR ONLY
# ---------------------------------------------------------
with tab_f:
    st.header("Calculate Darcy Friction Factor")
    
    Re_f = st.number_input("Reynolds Number", value=100000.0, step=1000.0, key="f_re")
    d_f = st.number_input("Pipe Diameter (m)", value=0.05, format="%.4f", key="f_d")
    e_f = st.number_input("Pipe Roughness (m)", value=0.000045, format="%.6f", key="f_e")

    if st.button("Calculate Friction Factor", use_container_width=True):
        f_val = friction_factor(Re_f, e_f, d_f)
        st.success(f"**Darcy Friction Factor (f):** {f_val:.6f}")


# ---------------------------------------------------------
# TAB 4: HEAD LOSS ONLY
# ---------------------------------------------------------
with tab_hf:
    st.header("Calculate Darcy-Weisbach Head Loss")
    
    c1, c2 = st.columns(2)
    f_hf = c1.number_input("Darcy Friction Factor", value=0.02, format="%.4f", key="hf_f")
    l_hf = c2.number_input("Pipe Length (m)", value=10.0, key="hf_l")
    d_hf = c1.number_input("Pipe Diameter (m)", value=0.05, format="%.4f", key="hf_d")
    v_hf = c2.number_input("Velocity (m/s)", value=2.0, key="hf_v")

    if st.button("Calculate Head Loss", use_container_width=True):
        hf_val = head_loss(f_hf, l_hf, d_hf, v_hf)
        st.success(f"**Head Loss (h_f):** {hf_val:.4f} m")


# ---------------------------------------------------------
# TAB 5: PRESSURE DROP ONLY
# ---------------------------------------------------------
with tab_dp:
    st.header("Calculate Pressure Drop")
    
    c1, c2 = st.columns(2)
    rho_dp = c1.number_input("Density (kg/m³)", value=1000.0, key="dp_rho")
    f_dp = c2.number_input("Darcy Friction Factor", value=0.02, format="%.4f", key="dp_f")
    l_dp = c1.number_input("Pipe Length (m)", value=10.0, key="dp_l")
    d_dp = c2.number_input("Pipe Diameter (m)", value=0.05, format="%.4f", key="dp_d")
    v_dp = st.number_input("Velocity (m/s)", value=2.0, key="dp_v")

    if st.button("Calculate Pressure Drop", use_container_width=True):
        hf_calc = head_loss(f_dp, l_dp, d_dp, v_dp)
        dp_pa = pressure_drop(rho_dp, hf_calc)
        dp_kpa = pascal_to_kpa(dp_pa)

        col_a, col_b, col_c = st.columns(3)
        col_a.metric("Head Loss", f"{hf_calc:.4f} m")
        col_b.metric("Pressure Drop (Pa)", f"{dp_pa:,.2f} Pa")
        col_c.metric("Pressure Drop (kPa)", f"{dp_kpa:.4f} kPa")
