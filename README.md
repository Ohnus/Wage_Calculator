# Wage_Calculator

import streamlit as st

st.write("""
# Monthly Pay Calculator　　　　　　　　　　　for part-time Workers in Korea
- Programmer: Ohnus
- File created: 12.08.2021
- File updated: 13.08.2021
""")
st.write('----')


st.write('''## This program caculates your monthly pay.''')
st.write('''- This is a simple program that part-time workers in Korea can calculate thier monthly pay conveniently.''' )
st.write('''- This will calculate your monthly pay in consideration of your holiday pay.''')
st.write('''- You don't have to input ***the [Number of Working Day in a month] column***,　　　　　　　　　if you work ***15 hours or more a week*** and ***60 hours or more a month***.''')
st.write('''- On the contrary, it's necessary to input ***the [Number of Working Day in a month] column***,　　 if you work ***less than 15 hours a week***.''')
st.write('----')

def main():
    st.write('''## Input Your Wage and Working Hours''')
    x = st.number_input("· Hourly wage (won)", min_value=0, max_value=30000)
    y = st.number_input("· Daily Working Hours", min_value=float(0), max_value=float(8))
    z = st.number_input("· Number of Working Day in a week", min_value=float(0), max_value=float(7))
    if y * z < 15:
        a = st.number_input("· Number of Working Day in a month", min_value=0, max_value=31)
        Month_Pay_PBT_Under15 = x*y*a
        Month_Pay_PAT_Under15 = x*y*a*0.967
        Income_Tax = x*y*a*0.033

    elif y * z >= 15:
        Month_Pay_PBT_Greater_than_or_equal_to_15 = (x*y*z*4.35417) + (x*8*4.35417)
        Month_Pay_PAT_Greater_than_or_equal_to_15 = ((x*y*z*4.35417) + (x*8*4.35417)) - (((x*y*z*4.35417) + (x*8*4.35417)) * 0.045) - (((x*y*z*4.35417) + (x*8*4.35417)) * 0.0343) - ((((x*y*z*4.35417) + (x*8*4.35417)) * 0.0343) * 0.1152) - (((x*y*z*4.35417) + (x*8*4.35417)) * 0.008)

        National_Pension_Plan = (((x*y*z*4.35417) + (x*8*4.35417)) * 0.045)
        Health_Insurance_Plus_Care_Insurance = (((x*y*z*4.35417) + (x*8*4.35417)) * 0.0343) * 1.1152
        Imployment_Insurance = (((x*y*z*4.35417) + (x*8*4.35417)) * 0.008)
        Occupational_Health_and_Safety_insurance = (((x*y*z*4.35417) + (x*8*4.35417)) * 0)

    st.write('''## Check your monthly pay''')

    if y * z < 15:
        st.write("· Your pay before tax is ***{:,.0f}won***.".format(Month_Pay_PBT_Under15))
        st.write("· Your pay after tax is ***{:,.0f}won***.".format(Month_Pay_PAT_Under15))
        st.write("· Income tax : ***{:,.0f}won***.".format(Income_Tax))

    elif y * z >= 15:
        st.write("· Your pay before four major insurance deductions is ***{:,.0f}won***.".format(Month_Pay_PBT_Greater_than_or_equal_to_15))
        st.write("· Your pay after four major insurance deductions is ***{:,.0f}won***.".format(Month_Pay_PAT_Greater_than_or_equal_to_15))
        st.write('''- Four Major insurance you pay''')
        st.write("1) National pension plan : ***{:,.0f}won***.".format(National_Pension_Plan))
        st.write("2) Health insurance and Care insurance : ***{:,.0f}won***.".format(Health_Insurance_Plus_Care_Insurance))
        st.write("3) Imployment insurance : ***{:,.0f}won***.".format(Imployment_Insurance))
        st.write("4) Occupational health and Safety insurance : ***{:,.0f}won***.".format(Occupational_Health_and_Safety_insurance))

    st.write('----')

main()
