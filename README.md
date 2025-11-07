# oneEHR


🧠 Data Model

State Object

state = {
  selections: {
    left: new Set(),
    right: new Set()
  },
  budget: {
    left: 4,
    right: 4
  }
}


Each button has attributes:

 - data-id → unique ID (e.g., L1, R3)

 - data-side → which panel it belongs to (left / right)

 - data-cost → numeric cost used for budget validation

🔄 How Mutex is Enforced

The MUTEX configuration defines pairs that cannot be selected together on the same side:

const MUTEX = {
  left: [['L1','L2'], ['L3','L4'], ['L5','L6']],
  right: [['R1','R2'], ['R3','R4'], ['R5','R6']]
};


When a button is selected:

 - Its mutex pair (on the same side) is automatically deselected.

 - Its opposite-side match (L1 ↔ R1, L2 ↔ R2, etc.) is also deselected.

 - Selection is blocked if it exceeds the side’s budget limit (4).

💾 Where State is Persisted

 - State is saved in localStorage under the key selector-state.

 - On reload, previous selections are restored automatically:

 - localStorage.setItem('selector-state', JSON.stringify(...));


Clicking Reset All clears both panels and removes saved state.

🧰 Features

 - Accessible via keyboard (Enter/Space toggles selection)

 - Visual feedback for selection and budget errors

 - Responsive layout for mobile and desktop

 - Toast notifications for over-budget or reset actions
