# EmpowerHer
A platform for teen girls and young women to learn how to lead with confidence.


## 🚀 Specification Deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [x] Proper use of Markdown
- [x] A concise and compelling elevator pitch
- [x] Description of key features
- [x] Description of how you will use each technology
- [x] One or more rough sketches of your application. Images must be embedded in this file using Markdown image references.

### Elevator pitch

EmpowerHer is a supportive website for teen girls and young women to learn about safety, boundaries, leadership, confidence, and mental wellness. Members read bite-size lessons, share real experiences in topic circles, and encourage each other with kind, constructive comments. Optional AI helps draft respectful boundary scripts and confidence prompts, while curated resources keep crisis help one click away. It’s a gentle, private, and uplifting space — education first, community always.


### Design

#### Home Design
![Home Design image](Home_Page.png)

#### Topic Circles
![Topic Circles Design image](Topic_Circles.png)

#### Micro-Lessons & Exercises
![Micro-Lessons Design image](Micro-lessons_&_Exercises.png)

#### Boundary Script Builder
![Boundary Script Builder Design image](Boundary_Script_Builder.png)

#### Leader Spotlight
![Leader Spotlight Design image](Leader_Spotlight.png)

#### Private Journnal
![Private Journal Design image](Private_Journal.png)



```mermaid
sequenceDiagram
  autonumber
  actor U as Member
  participant FE as Frontend (React)
  participant API as Backend (Express)
  participant DB as Database
  participant WS as WebSocket

  U->>FE: Open /post/:id
  FE->>API: GET /api/posts/:id
  API->>DB: Fetch post + comments
  DB-->>API: Rows
  API-->>FE: 200 (post, comments)
  FE->>WS: join post:{id}

  U->>FE: Submit comment
  FE->>API: POST /api/posts/:id/comments {body}
  API->>DB: Insert comment
  DB-->>API: OK
  API-->>FE: 201 (comment)
  API-->>WS: emit comment:created {postId, comment}
  WS-->>FE: broadcast to all in post:{id}

```


```mermaid
sequenceDiagram
  autonumber
  actor U as Member
  participant FE as React
  participant API as Backend
  participant AI as AI Provider
  participant DB as Database

  U->>FE: Open Boundary Builder, fill scenario + tone
  FE->>API: POST /api/ai/boundary {scenario, tone}
  API->>AI: (optional) Generate non-clinical scripts
  AI-->>API: Suggestions
  API->>DB: Save suggestions (optional)
  DB-->>API: OK
  API-->>FE: 200 {scripts:[...], checklist:[...]}

```


```mermaid
sequenceDiagram
  autonumber
  participant FE as React
  participant API as Backend
  participant EXT as Public APIs (Quotable/Wikipedia)

  FE->>API: GET /api/affirmation
  API->>EXT: Fetch affirmation
  EXT-->>API: JSON
  API-->>FE: 200 {text, author}

  FE->>API: GET /api/spotlight/today
  API->>EXT: Fetch leader summary
  EXT-->>API: JSON
  API-->>FE: 200 {name, summary, thumbnail}

```


```mermaid
sequenceDiagram
  autonumber
  actor U as User
  participant FE as Frontend (React)
  participant API as Backend (Express)
  participant EXT as Quotes API
  participant DB as Database

  U->>FE: POST /api/auth/login (email, password)
  FE->>API: /api/auth/login
  API-->>FE: 200 (set HTTP-only session cookie)

  U->>FE: Redirect to /dashboard
  FE->>API: GET /api/affirmation (with session cookie)
  API->>DB: read recent user quote history (optional)
  API->>EXT: fetch random inspirational quote (server-side)
  EXT-->>API: quote JSON
  API->>DB: save (user_id, quote_id/text_hash)
  API-->>FE: 200 { text, author, id }
  FE-->>U: Render Affirmation card (Save/Share actions)

```


### Key features

- **Secure authentication over HTTPS**: register, login, logout
- **Create style questions with images**: upload one or more images of clothing items and ask: "How would you style this?"
- **Community responses with images**: respondents can upload inspo photos or outfit mockups with comments on how to style clothing items
- **Ranked voting (top 3)**: the top three comments/responses with the most votes will be highlighted
- **Realtime tallies**: as votes come in, everyone sees tallies update instantly (WebSocket)
- **AI style and beauty advice**: optional AI suggestions
- **Show the final look**: creator posts final outfit in response to their question
- **Admin tools**: create/close/delete questions, moderate content, ban abuse
- **Persistent results**: posts, responses, votes and AI suggestions are stored and queryable

### Technologies

I am going to use the required technologies in the following ways.

**HTML**
- Single HTML entry (index.html) for a React SPA (desktop-first layout; also responsive down to tablet/phone)
- Semantic structure for header, nav, main, footer, accessible forms and labels
- Web meta: viewport, Open Graph, and favicon to API/CDN

**CSS** 
- Desktop-first CSS Grid/Flex layout; breakouts for tablet/phone
- Design tokens for color/spacing/typography; high contrast for readability
- Hover/focus/active states; visible focus rings
- Image handling: responsive max-width: 100%, object-fit, and a simple lightbox on desktop

**React** 
- Stack: React + react-router-dom
- Routes: / (feed), /login, /register, /create, /post/:id, /profile, /admin
- Components: Navbar, AuthForm, PostCard, PostDetail, ResponseCard, Top3Picker (HTML5 DnD + keyboard), TallyPanel, Uploader, AiAdvicePanel, AdminDashboard
- Perf: code-split heavy views with React.lazy; prefetch data on hover for desktop
- A11y: Proper ARIA for lists/cards, drag handles, live region updates on tally changes

**Service** 
- Stack
- Security for browsers
- Auth
- Uploads
- Posts/Responses
- Voting
- AI and public API: calls AI provider server-side and returns normalized tips

**DB/Login** 
- Postgres, MySQL, or MongoDB
- Schema
- Indexes
- Tallies: compute on read or cache weighted scores

**WebSocket**
- Room per post: post:{postID}
- Client subscribes when mounts, cleans up on unmount


## 🚀 AWS deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **Server deployed and accessible with custom domain name** - [My server link](https://yourdomainnamehere.click).

## 🚀 HTML deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **HTML pages** - I did not complete this part of the deliverable.
- [ ] **Proper HTML element usage** - I did not complete this part of the deliverable.
- [ ] **Links** - I did not complete this part of the deliverable.
- [ ] **Text** - I did not complete this part of the deliverable.
- [ ] **3rd party API placeholder** - I did not complete this part of the deliverable.
- [ ] **Images** - I did not complete this part of the deliverable.
- [ ] **Login placeholder** - I did not complete this part of the deliverable.
- [ ] **DB data placeholder** - I did not complete this part of the deliverable.
- [ ] **WebSocket placeholder** - I did not complete this part of the deliverable.

## 🚀 CSS deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **Header, footer, and main content body** - I did not complete this part of the deliverable.
- [ ] **Navigation elements** - I did not complete this part of the deliverable.
- [ ] **Responsive to window resizing** - I did not complete this part of the deliverable.
- [ ] **Application elements** - I did not complete this part of the deliverable.
- [ ] **Application text content** - I did not complete this part of the deliverable.
- [ ] **Application images** - I did not complete this part of the deliverable.

## 🚀 React part 1: Routing deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **Bundled using Vite** - I did not complete this part of the deliverable.
- [ ] **Components** - I did not complete this part of the deliverable.
- [ ] **Router** - I did not complete this part of the deliverable.

## 🚀 React part 2: Reactivity deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **All functionality implemented or mocked out** - I did not complete this part of the deliverable.
- [ ] **Hooks** - I did not complete this part of the deliverable.

## 🚀 Service deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **Node.js/Express HTTP service** - I did not complete this part of the deliverable.
- [ ] **Static middleware for frontend** - I did not complete this part of the deliverable.
- [ ] **Calls to third party endpoints** - I did not complete this part of the deliverable.
- [ ] **Backend service endpoints** - I did not complete this part of the deliverable.
- [ ] **Frontend calls service endpoints** - I did not complete this part of the deliverable.
- [ ] **Supports registration, login, logout, and restricted endpoint** - I did not complete this part of the deliverable.


## 🚀 DB deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **Stores data in MongoDB** - I did not complete this part of the deliverable.
- [ ] **Stores credentials in MongoDB** - I did not complete this part of the deliverable.

## 🚀 WebSocket deliverable

For this deliverable I did the following. I checked the box `[x]` and added a description for things I completed.

- [ ] **Backend listens for WebSocket connection** - I did not complete this part of the deliverable.
- [ ] **Frontend makes WebSocket connection** - I did not complete this part of the deliverable.
- [ ] **Data sent over WebSocket connection** - I did not complete this part of the deliverable.
- [ ] **WebSocket data displayed** - I did not complete this part of the deliverable.
- [ ] **Application is fully functional** - I did not complete this part of the deliverable.
