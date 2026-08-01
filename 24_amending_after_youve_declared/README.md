# 24 · Amending After You've Declared

**Tier 3** · Target length **0:45**

> Reopening a declared year while HMRC's amendment window is open.

**Script:** [`script.html`](script.html) — written.

**Staging:** load **demo scene 24** (`/dashboard/demo-scenes`) right before recording. It stages 2025-26 as fully declared — app-side compliance history *and* the HMRC mock flipped so the final-declaration obligation shows Fulfilled (20 Jul 2026). The mock then plays the amendment as a story: requesting **Intent to Amend** reopens the 2025-26 obligation (beat 2's "year reopens" shot) and adds the processed intent-to-amend calculation; submitting the confirmation closes the year again for the calm closer. Retake? Reload scene 24 — it resets the sequence. Needs the api image built on/after 1 Aug 2026 and the updated WireMock fixtures shipped to the server. Loading any other scene reverts the mock to the pre-declaration state video 6 needs.

Finished video files go in this folder alongside the script.

## Checklist

- [x] Script written
- [ ] Screens staged & recorded (Ritchie)
- [ ] Edit + voiceover (creator)
- [ ] Final video delivered to this folder
- [ ] Published
