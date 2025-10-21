# Cambridge YLE Online Tests Platform

A comprehensive, interactive testing platform for Cambridge Young Learners English (YLE) examinations.

## 🚀 Quick Start Guide

### Prerequisites
- GitHub account
- Git installed on your computer
- Basic text editor (VS Code recommended)
- Web browser

### Phase 1: Initial Setup

#### 1. Create GitHub Repository
```bash
# On GitHub.com:
# 1. Click "+" → "New repository"
# 2. Name: cambridge-yle-tests
# 3. Public repository
# 4. Add README
# 5. Create repository
```

#### 2. Clone Repository Locally
```bash
git clone https://github.com/YOUR_USERNAME/cambridge-yle-tests.git
cd cambridge-yle-tests
```

#### 3. Create Project Structure
```bash
# Create directories
mkdir -p pages assets/css assets/js assets/images assets/audio data/tests

# Create initial files
touch index.html
touch pages/test-selection.html
touch pages/listening.html
touch pages/reading-writing.html
touch pages/results.html
touch assets/css/style.css
touch assets/js/main.js
touch assets/js/test-engine.js
touch assets/js/audio-player.js
```

#### 4. Enable GitHub Pages
1. Go to repository Settings
2. Navigate to "Pages" section
3. Source: Deploy from branch "main"
4. Folder: "/ (root)"
5. Save

Your site will be live at: `https://YOUR_USERNAME.github.io/cambridge-yle-tests`

---

## 📁 Project Structure

```
cambridge-yle-tests/
├── index.html                    # Landing page (level selection)
├── pages/
│   ├── test-selection.html      # Test number selection
│   ├── listening.html           # Listening test interface
│   ├── reading-writing.html     # Reading & Writing interface
│   └── results.html             # Results and feedback page
├── assets/
│   ├── css/
│   │   └── style.css           # Main stylesheet
│   ├── js/
│   │   ├── main.js             # Core functionality
│   │   ├── test-engine.js      # Test logic & validation
│   │   └── audio-player.js     # Audio controls
│   ├── images/                  # Test images, illustrations
│   └── audio/                   # Listening test audio files
├── data/
│   └── tests/                   # Test data JSON files
│       ├── starters/
│       ├── movers/
│       └── flyers/
└── README.md
```

---

## 🔨 Phase 2: Building the Platform

### Step 1: Add Landing Page
Copy the provided `index.html` to your repository root.

### Step 2: Add Test Selection Page
Copy the provided `test-selection.html` to the `pages/` directory.

### Step 3: Create Listening Test Interface

Create `pages/listening.html`:
- Audio player with controls (play, pause, replay, forward)
- Interactive question areas (drag-and-drop, multiple choice, matching)
- Progress indicator
- Submit and check answers functionality
- Timer (optional)

### Step 4: Create Reading & Writing Interface

Create `pages/reading-writing.html`:
- Text passages with images
- Various question types:
  - Multiple choice
  - Fill in the blanks
  - Matching exercises
  - Short answer questions
- Image-based questions
- Word bank for writing tasks

### Step 5: Create Results Page

Create `pages/results.html`:
- Score calculation and display
- Section-by-section breakdown
- Correct/incorrect answer review
- Performance feedback
- Option to retake or try another test
- Progress chart

### Step 6: Test Data Structure

Create JSON files for each test in `data/tests/[level]/test_[number].json`:

```json
{
  "level": "flyers",
  "testNumber": 1,
  "listening": {
    "parts": [
      {
        "partNumber": 1,
        "instructions": "Listen and draw lines...",
        "audioFile": "../../assets/audio/flyers/test1/part1.mp3",
        "questions": [
          {
            "id": "L1_Q1",
            "type": "matching",
            "items": ["Katy", "Robert", "Oliver"],
            "options": ["playing football", "reading", "swimming"],
            "answer": {"Katy": "swimming", "Robert": "reading", "Oliver": "playing football"}
          }
        ]
      }
    ]
  },
  "readingWriting": {
    "parts": [
      {
        "partNumber": 1,
        "instructions": "Look and read. Choose the correct words...",
        "questions": [
          {
            "id": "RW1_Q1",
            "type": "multiple_choice",
            "question": "You can buy stamps here.",
            "options": ["post office", "library", "museum"],
            "answer": "post office"
          }
        ]
      }
    ]
  }
}
```

---

## 🎨 Phase 3: JavaScript Implementation

### Main Features to Implement

#### 1. Test Engine (`assets/js/test-engine.js`)
```javascript
class TestEngine {
  constructor(testData) {
    this.testData = testData;
    this.userAnswers = {};
    this.startTime = Date.now();
  }

  recordAnswer(questionId, answer) {
    this.userAnswers[questionId] = answer;
    this.saveProgress();
  }

  checkAnswers() {
    // Compare user answers with correct answers
    // Calculate score
    // Return results object
  }

  saveProgress() {
    // Save to localStorage
  }

  loadProgress() {
    // Load from localStorage
  }
}
```

#### 2. Audio Player (`assets/js/audio-player.js`)
```javascript
class AudioPlayer {
  constructor(audioElement) {
    this.audio = audioElement;
    this.setupControls();
  }

  play() { }
  pause() { }
  replay() { }
  forward(seconds) { }
  updateProgress() { }
}
```

#### 3. Results Tracking
```javascript
class ResultsTracker {
  saveResult(level, testNum, section, score, answers) {
    const key = `test_${level}_${testNum}_${section}`;
    localStorage.setItem(key, JSON.stringify({
      score,
      answers,
      date: new Date().toISOString(),
      completed: true
    }));
  }

  getHistory(level) {
    // Return all completed tests for a level
  }

  calculateOverallProgress(level) {
    // Calculate average score, tests completed, etc.
  }
}
```

---

## 📊 Phase 4: Data Collection Features

### Client-Side Storage (localStorage)
Store test results locally for each user:

```javascript
// Structure for stored data
{
  "test_flyers_1_listening": {
    "score": 85,
    "totalQuestions": 25,
    "correctAnswers": ["L1_Q1", "L1_Q2", ...],
    "incorrectAnswers": ["L2_Q3", ...],
    "timeSpent": 1234567, // milliseconds
    "completedDate": "2025-10-21T10:30:00Z"
  },
  "userProfile": {
    "name": "Optional",
    "totalTestsCompleted": 5,
    "averageScore": 82,
    "preferredLevel": "flyers"
  }
}
```

### Optional: Server-Side Data Collection
For collecting aggregated data across users:

1. **Option A: Google Sheets API**
   - Free and simple
   - Create a Google Form/Sheet
   - Submit results via API

2. **Option B: Firebase**
   - Real-time database
   - User authentication
   - Analytics dashboard

3. **Option C: Simple Backend**
   - Node.js + Express
   - PostgreSQL/MongoDB
   - Deploy on Heroku/Railway

---

## 🎯 Phase 5: Key Features Implementation

### Feature 1: Drag and Drop (Listening Part 1)
```javascript
// Implement with HTML5 Drag and Drop API
element.addEventListener('dragstart', handleDragStart);
element.addEventListener('drop', handleDrop);
```

### Feature 2: Audio Synchronization
- Highlight current question when audio plays
- Auto-advance to next question
- Replay specific sections

### Feature 3: Answer Validation
- Real-time feedback
- Explanation for correct answers
- Tips for improvement

### Feature 4: Progress Tracking
- Visual progress bars
- Completed vs. incomplete tests
- Score history charts
- Achievement badges

---

## 🚢 Phase 6: Deployment

### Commit and Push to GitHub
```bash
# Add all files
git add .

# Commit changes
git commit -m "Initial commit: Cambridge YLE testing platform"

# Push to GitHub
git push origin main
```

### Verify GitHub Pages Deployment
1. Wait 2-3 minutes for deployment
2. Visit: `https://YOUR_USERNAME.github.io/cambridge-yle-tests`
3. Test all functionality

---

## 📝 Development Checklist

### Phase 1: Setup ✓
- [ ] Create GitHub repository
- [ ] Clone locally
- [ ] Create folder structure
- [ ] Enable GitHub Pages

### Phase 2: Core Pages
- [ ] Landing page (index.html)
- [ ] Test selection page
- [ ] Listening test interface
- [ ] Reading & Writing interface
- [ ] Results page

### Phase 3: Functionality
- [ ] Test data loading
- [ ] Answer recording
- [ ] Audio player controls
- [ ] Answer validation
- [ ] Score calculation
- [ ] Progress saving

### Phase 4: Test Content
- [ ] Create test data JSON files
- [ ] Add audio files
- [ ] Add images
- [ ] Verify all answers

### Phase 5: Polish
- [ ] Responsive design
- [ ] Cross-browser testing
- [ ] Performance optimization
- [ ] Error handling
- [ ] User instructions

### Phase 6: Advanced Features
- [ ] Data export functionality
- [ ] Print results option
- [ ] Dark mode
- [ ] Accessibility features (ARIA labels, keyboard navigation)
- [ ] Multi-language support

---

## 🎨 Design Guidelines

### Color Schemes
- **Starters (Pre-A1)**: Green/Blue gradients (#84fab0 → #8fd3f4)
- **Movers (A1)**: Purple/Pink gradients (#a18cd1 → #fbc2eb)
- **Flyers (A2)**: Orange/Peach gradients (#ffecd2 → #fcb69f)

### Typography
- Headers: 2rem - 2.5rem
- Body: 1rem - 1.1rem
- Buttons: 1rem, bold

### UI Principles
- Large, touch-friendly buttons
- Clear visual feedback
- Child-friendly illustrations
- Simple navigation
- Encouraging messages

---

## 🔧 Testing Your Platform

### Manual Testing Checklist
1. [ ] All navigation links work
2. [ ] Audio plays correctly
3. [ ] Answers are recorded
4. [ ] Scores calculate correctly
5. [ ] Progress saves and loads
6. [ ] Responsive on mobile
7. [ ] Works in different browsers

### Browser Compatibility
- Chrome ✓
- Firefox ✓
- Safari ✓
- Edge ✓
- Mobile browsers ✓

---

## 📚 Resources Needed

### Audio Files
- Record or source Cambridge YLE-style audio
- Format: MP3, 128kbps
- Duration: 1-3 minutes per part

### Images
- Test illustrations
- Character icons
- UI elements
- Backgrounds

### Test Content
- Official Cambridge YLE practice materials
- Create custom questions following Cambridge format
- Ensure copyright compliance

---

## 🚀 Next Steps After Basic Platform

1. **Add More Tests**: Create all 8 tests for each level
2. **Gamification**: Add points, badges, leaderboards
3. **Teacher Dashboard**: For tracking student progress
4. **Export Results**: PDF reports
5. **Offline Mode**: Service workers for offline access
6. **Mobile App**: Convert to PWA or native app
7. **Community Features**: Share scores, compete with friends

---

## 💡 Tips for Success

1. **Start Small**: Build one complete test first
2. **Test Often**: Check functionality after each feature
3. **User Feedback**: Get real students to test
4. **Iterate**: Improve based on feedback
5. **Document**: Keep code well-commented
6. **Backup**: Regular commits to GitHub

---

## 🆘 Troubleshooting

### GitHub Pages Not Working
- Check repository is public
- Verify Pages is enabled in Settings
- Wait 5-10 minutes after first push
- Check for errors in Actions tab

### Audio Not Playing
- Check file paths are correct
- Use relative paths: `../../assets/audio/...`
- Verify MP3 format compatibility
- Check browser console for errors

### Styles Not Loading
- Verify CSS file paths
- Check for syntax errors in CSS
- Hard refresh browser (Ctrl+F5)
- Check browser developer tools

---

## 📞 Support

For questions or issues:
1. Check GitHub Issues tab
2. Review browser console errors
3. Validate HTML/CSS/JS syntax
4. Test in different browsers

---

## 📄 License

MIT License - Feel free to use and modify for educational purposes.

---

## 🎓 Educational Use

This platform is designed for:
- Independent learners practicing for Cambridge YLE exams
- Teachers supplementing classroom instruction
- Parents supporting their children's English learning
- Language schools providing practice materials

**Note**: This is a practice platform. Official Cambridge certificates can only be obtained through authorized examination centers.

---

Happy coding! 🚀 You're building something that will help thousands of young learners improve their English skills!