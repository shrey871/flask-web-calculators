
import streamlit as st
import pandas as pd

st.set_page_config(page_title="Shopping Discount Calculator", page_icon="🛒")

st.title("🛒 Shopping Discount Calculator")

# Create history
if "history" not in st.session_state:
    st.session_state.history = []

# Customer Details
name = st.text_input("Customer Name")

amount = st.number_input(
    "Purchase Amount (₹)",
    min_value=0.0,
    format="%.2f"
)

membership = st.selectbox(
    "Membership Type",
    ["Regular", "Silver", "Gold", "Platinum"]
)

# Discount Rates
discounts = {
    "Regular": 5,
    "Silver": 10,
    "Gold": 15,
    "Platinum": 20
}

if st.button("Calculate Discount"):

    discount_rate = discounts[membership]

    discount_amount = amount * discount_rate / 100
    final_amount = amount - discount_amount

    st.success("Calculation Completed!")

    st.write(f"**Customer Name:** {name}")
    st.write(f"**Purchase Amount:** ₹{amount:.2f}")
    st.write(f"**Membership:** {membership}")
    st.write(f"**Discount:** {discount_rate}%")
    st.write(f"**Discount Amount:** ₹{discount_amount:.2f}")
    st.write(f"### Final Payable Amount: ₹{final_amount:.2f}")

    # Save history
    st.session_state.history.append({
        "Customer": name,
        "Purchase Amount": amount,
        "Membership": membership,
        "Discount %": discount_rate,
        "Discount Amount": discount_amount,
        "Final Amount": final_amount
    })

# Display History
st.subheader("📜 Transaction History")

if st.session_state.history:
    df = pd.DataFrame(st.session_state.history)
    st.dataframe(df, use_container_width=True)
else:
    st.info("No transactions yet.")


















