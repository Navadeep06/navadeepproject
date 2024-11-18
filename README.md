import streamlit as st
import random

# Initialize or reset game state
if 'number' not in st.session_state:
    st.session_state.number = random.randint(1, 100)
    st.session_state.attempts = 0
    st.session_state.message = "Guess a number between 1 and 100!"

# Title
st.title("Guess the Number Game")

# Display the message
st.write(st.session_state.message)

# Input for guessing
guess = st.number_input("Enter your guess:", min_value=1, max_value=100, step=1)
if st.button("Submit Guess"):
    st.session_state.attempts += 1  # Increment attempts
    if guess < st.session_state.number:
        st.session_state.message = "Too low! Try again."
    elif guess > st.session_state.number:
        st.session_state.message = "Too high! Try again."
    else:
        st.session_state.message = (
            f"🎉 Congratulations! You guessed it in {st.session_state.attempts} attempts."
        )
        # Reset game for a new round
        st.session_state.number = random.randint(1, 100)
        st.session_state.attempts = 0

# Show the updated message
st.write(st.session_state.message)


