# Lost in Time challenge-writeup



# Lost in Time?

**Category:** OSINT  
**CTF Type:** OSINT  
**Difficulty / Segment:** 2 (easy)  
**PoV:** Blue / Analyst  
**Job Role:** Security Analyst / Blue Team  
**Skills:** OSINT, Geolocation, Image Analysis, Critical Thinking  
**Technologies:** Google Maps, Google Street View, Reverse Image Search, Browser Tools

---

## Challenge
A street. A moment. Your move.

(An image `street.png` was provided. No further hints were given.)

**Objective:**  
Using OSINT techniques, complete this CTF task by analyzing the provided street photo to determine the location’s timezone.

**Flag format:**  
FLAG{UTC/GMT -8 hours}


---

## Tools used
- Modern web browser (Chrome / Firefox)  
- Google Images / Reverse image search (images.google.com / tineye)  
- Google Maps / Google Street View  
- `exiftool` (for verification—confirm image metadata was removed)  
- `convert` / ImageMagick (optional cropping/resize during analysis)

---

## Walkthrough (spoilers)
<details>
<summary>Click to reveal the step-by-step solution</summary>

1. **Initial inspection**
   - Open `street.png` and look for visual clues: shop signs, language/script, vehicle styles, bus stops, road markings, phone codes, area codes, visible business names, and architecture.
   - Note conspicuous items but don't rely on a single small text fragment (it may be cropped or partial).

2. **Sanity check for metadata**
   - Run:
     ```bash
     exiftool street.png
     ```
     to ensure there is no embedded GPS/EXIF data. For a properly sanitized image, this should show no GPS coordinates.

3. **Reverse image search**
   - Use Google Images (images.google.com) or TinEye:
     - Upload `street.png` and look for exact or visually similar matches.
     - Often a good reverse image result yields social media posts, blog posts, or map screenshots that reveal the location or clues.

4. **Zoom in on readable text**
   - If any partial text is visible (shop name, phone number partial), crop the image to that region and run a targeted reverse image search or search the text string in Google.
   - Example cropping with ImageMagick (optional):
     ```bash
     convert street.png -crop 800x400+100+200 cropped.png
     ```
     Then reverse image search `cropped.png`.

5. **Use map services**
   - If a landmark or shop name is discovered, search it in Google Maps.
   - Use Google Street View to visually match the scene. Look for the same storefronts, road markings, or street furniture.

6. **Confirm the city**
   - Once the city (or precise locality) is identified via matching business/landmarks/street layout, confirm its administrative region (state/county) using Google Maps.

7. **Determine the timezone**
   - Once the city is confirmed (e.g., Hanford, California), map it to its timezone:
     - Hanford, CA is in the Pacific Time Zone.
     - Standard time for Pacific Time = **UTC/GMT −8 hours** (PST).
     - Daylight saving (PDT) = UTC−7, but the challenge expects the standard offset.

8. **Submit the flag**
   - Submit the exact string required by the challenge:
     ```
     FLAG{UTC/GMT -8 hours}
     ```

</details>

---

## Solution (final)
FLAG{UTC/GMT -8 hours}


---

## Notes & authoring remarks
- The challenge intentionally used a sanitized Google Maps screenshot to force solvers to rely on visual clues and mapping resources rather than embedded metadata.
- For clarity to participants, the task states to use OSINT techniques and expects the timezone as the answer. If you want to avoid DST confusion, explicitly require the **standard time offset** (UTC−8) in the task text (as is done here).
- If you reuse online map screenshots, always remove EXIF and crop/blur direct coordinate readouts or map overlays so the problem remains investigative, not trivial.

---

if you have a problem don't hesitate and send me a message, discord : redeex

**Author:** Official writeup for the `What Time Is It?` challenge  
**License:** CC0 — public domain (use freely)
