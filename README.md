# Background

The original **Botox M365 firmware** has a bug when using the custom Russian throttle algorithm. This bug causes the scooter to lack torque at very low speeds. More information about this issue can be found [here](https://github.com/BotoX/xiaomi-m365-firmware-patcher/issues/61).

The **ScooterHacking firmware** fixes this problem, but it introduces another issue — at least for my use case.

## The "Clonk-Free" KERS Issue

The feature is called **"Clonk-Free KERS"**.

Unlike Botox firmware, where setting KERS to a high value (for example, **40 km/h**) completely disables the motor, allowing the scooter to freely coast downhill without a speed limit, ScooterHacking firmware keeps the motor active.

The reason for this is to prevent the scooter from jerking or making a **"clonk"** sound when the throttle is pressed again. This noise happens when the motor wakes up after being completely turned off.

To achieve this smoother behavior, ScooterHacking keeps the motor running and applies a very small amount of current — only a few watts — just enough to keep the motor spinning and reduce friction.

The downside is that keeping the motor active creates a speed limitation due to the motor's **back EMF**.

Because of this the maximum downhill/coasting speed is reduced to around **33 km/h** and when the battery voltage is low, this limit can drop to around **25 km/h**.

This limitation is annoying for my use case, which is why I wanted to achieve the best of both worlds:

- The improved low-speed torque from ScooterHacking firmware  
- The completely disabled motor behavior from Botox firmware when coasting  
- No artificial speed limitation from back EMF

# Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cd web/
python app.py