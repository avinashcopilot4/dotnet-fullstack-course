# 02 — HTML Forms & Inputs

> **Interview Tip:** Forms are the primary way users send data to a server. Understanding form structure, input types, and validation is essential for any front-end developer.

---

## Basic Form Structure

```html
<form action="/submit" method="POST">
  <!-- form elements go here -->
  <button type="submit">Submit</button>
</form>
```

| Attribute | Values | Meaning |
|---|---|---|
| `action` | URL | Where to send the data |
| `method` | `GET` / `POST` | How to send it |
| `enctype` | `multipart/form-data` | Required for file uploads |
| `novalidate` | — | Skips browser validation |

### GET vs POST

| | GET | POST |
|---|---|---|
| Data location | In the URL (`?name=Rahul`) | In the request body |
| Visible to user | Yes | No |
| Use case | Search, filters | Login, signup, file upload |
| Bookmarkable | Yes | No |
| Length limit | Yes (~2000 chars) | No |

> **Interview Q:** When do you use GET vs POST?
> — GET for reading/searching data; POST for sending sensitive or large data.

---

## The `<label>` Element

Always link a label to its input using `for` and `id`. This is **critical for accessibility**.

```html
<!-- Method 1: linked via for/id -->
<label for="username">Username:</label>
<input type="text" id="username" name="username" />

<!-- Method 2: wrapping -->
<label>
  Email:
  <input type="email" name="email" />
</label>
```

> Clicking the label automatically focuses/checks the input — improves UX especially on mobile.

---

## Input Types

### Text Inputs

```html
<input type="text"     name="name"    placeholder="Enter name" />
<input type="email"    name="email"   placeholder="you@example.com" />
<input type="password" name="pass"    />
<input type="number"   name="age"     min="1" max="120" />
<input type="tel"      name="phone"   placeholder="+91 9876543210" />
<input type="url"      name="website" placeholder="https://example.com" />
<input type="search"   name="query"   />
```

### Date & Time Inputs

```html
<input type="date"           name="dob" />
<input type="time"           name="meeting" />
<input type="datetime-local" name="event" />
<input type="month"          name="month" />
<input type="week"           name="week" />
```

### Choice Inputs

```html
<!-- Checkbox (multiple selections allowed) -->
<input type="checkbox" id="html" name="skills" value="html" />
<label for="html">HTML</label>

<input type="checkbox" id="css" name="skills" value="css" checked />
<label for="css">CSS</label>

<!-- Radio (only ONE selection from a group) -->
<input type="radio" id="male"   name="gender" value="male" />
<label for="male">Male</label>

<input type="radio" id="female" name="gender" value="female" />
<label for="female">Female</label>
```

> **Interview Q:** What's the difference between checkbox and radio?
> — Checkbox allows multiple selections; radio allows only one selection per group (same `name`).

### Special Inputs

```html
<input type="range"  name="volume" min="0" max="100" value="50" />
<input type="color"  name="theme" value="#ff0000" />
<input type="file"   name="resume" accept=".pdf,.doc" />
<input type="hidden" name="token" value="abc123" />
```

---

## Other Form Elements

### Textarea

```html
<label for="bio">Bio:</label>
<textarea
  id="bio"
  name="bio"
  rows="4"
  cols="40"
  placeholder="Tell us about yourself..."
  maxlength="500"
></textarea>
```

> Unlike `<input>`, `<textarea>` has a closing tag. Content goes between the tags, not in `value`.

### Select Dropdown

```html
<label for="city">City:</label>
<select id="city" name="city">
  <option value="">-- Select City --</option>
  <option value="hyd">Hyderabad</option>
  <option value="del">Delhi</option>
  <option value="mum" selected>Mumbai</option>
</select>

<!-- Multiple selections -->
<select name="languages" multiple size="4">
  <option value="js">JavaScript</option>
  <option value="py">Python</option>
  <option value="java">Java</option>
</select>

<!-- Grouped options -->
<select name="course">
  <optgroup label="Frontend">
    <option value="html">HTML</option>
    <option value="css">CSS</option>
  </optgroup>
  <optgroup label="Backend">
    <option value="node">Node.js</option>
  </optgroup>
</select>
```

### Datalist (Autocomplete Suggestions)

```html
<input list="browsers" name="browser" placeholder="Choose browser" />
<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Safari">
  <option value="Edge">
</datalist>
```

> Similar to `<select>` but allows free text entry too. The `list` attribute links input to datalist `id`.

---

## Button Types

```html
<button type="submit">Submit Form</button>   <!-- default, submits form -->
<button type="reset">Reset</button>          <!-- clears all fields -->
<button type="button">Click Me</button>      <!-- no default action, use with JS -->

<!-- Input as button (older style) -->
<input type="submit" value="Submit" />
<input type="reset"  value="Clear" />
<input type="image"  src="btn.png" alt="Submit" />
```

> **Interview Q:** What is the difference between `<button type="button">` and `<button type="submit">`?
> — `submit` sends the form; `button` does nothing by default (used with JavaScript).

---

## Form Validation Attributes

```html
<input
  type="email"
  name="email"
  required                 <!-- field cannot be empty -->
  minlength="5"            <!-- minimum characters -->
  maxlength="100"          <!-- maximum characters -->
  pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"  <!-- regex pattern -->
  placeholder="Enter email"
  title="Please enter a valid email"   <!-- shown on validation error -->
/>

<input type="number" name="age" min="18" max="60" step="1" required />
<input type="text"   name="pincode" pattern="[0-9]{6}" title="6-digit pincode" />
```

| Attribute | Purpose |
|---|---|
| `required` | Field must be filled |
| `minlength` / `maxlength` | Text length limits |
| `min` / `max` | Number/date range |
| `step` | Number increment |
| `pattern` | Regex pattern |
| `placeholder` | Hint text (not a label!) |
| `disabled` | Field is inactive and not submitted |
| `readonly` | Field shows value but cannot be edited |
| `autofocus` | Field is focused on page load |
| `autocomplete` | Browser suggests values (`on`/`off`) |

---

## Fieldset & Legend (Grouping)

```html
<form>
  <fieldset>
    <legend>Personal Information</legend>
    <label for="fname">First Name:</label>
    <input type="text" id="fname" name="fname" />

    <label for="lname">Last Name:</label>
    <input type="text" id="lname" name="lname" />
  </fieldset>

  <fieldset>
    <legend>Account Details</legend>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" />
  </fieldset>
</form>
```

> `<fieldset>` groups related fields visually and semantically. `<legend>` is the caption.

---

## Complete Registration Form Example

```html
<form action="/register" method="POST" enctype="multipart/form-data">
  <h2>Register</h2>

  <fieldset>
    <legend>Personal Info</legend>

    <label for="name">Full Name *</label>
    <input type="text" id="name" name="name" required minlength="2" placeholder="Rahul Sharma" />

    <label for="email">Email *</label>
    <input type="email" id="email" name="email" required placeholder="rahul@gmail.com" />

    <label for="phone">Phone</label>
    <input type="tel" id="phone" name="phone" pattern="[0-9]{10}" placeholder="9876543210" />

    <label for="dob">Date of Birth</label>
    <input type="date" id="dob" name="dob" />
  </fieldset>

  <fieldset>
    <legend>Account</legend>

    <label for="password">Password *</label>
    <input type="password" id="password" name="password" required minlength="8" />

    <label for="role">Role</label>
    <select id="role" name="role">
      <option value="">Select role</option>
      <option value="student">Student</option>
      <option value="developer">Developer</option>
    </select>

    <label for="resume">Upload Resume</label>
    <input type="file" id="resume" name="resume" accept=".pdf" />
  </fieldset>

  <label>
    <input type="checkbox" name="terms" required />
    I agree to the Terms & Conditions
  </label>

  <button type="submit">Register</button>
  <button type="reset">Clear</button>
</form>
```

---

## Common Interview Questions

1. What is the difference between `GET` and `POST` methods in a form?
2. What does `enctype="multipart/form-data"` do?
3. What is the role of `<label>` in a form?
4. What is the difference between `<input type="button">` and `<button type="submit">`?
5. How do you make a form field required using HTML?
6. What is the difference between `disabled` and `readonly` attributes?
7. What is a `<datalist>` element?
8. Why should `name` and `id` attributes have different purposes?
   - `name` — used to send data to server
   - `id` — used to link label, and accessed by JavaScript/CSS
