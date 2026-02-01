# CodeBuddy - AI Logic Tutor & Lab Assistant Requirements

## Project Overview

CodeBuddy is an AI-powered developer productivity tool designed specifically for students learning programming. Unlike traditional code-fixing tools, CodeBuddy focuses on logic explanation to help students understand why their code failed and how to improve their programming concepts.

## Target Users

- **Primary**: Computer Science students learning C and Python programming
- **Secondary**: Instructors and teaching assistants who want to understand common student mistakes
- **Tertiary**: Self-taught programmers seeking conceptual understanding

## Core Value Proposition

Transform debugging from frustration to learning by providing clear explanations of logic gaps and preparing students for academic assessments through AI-powered analysis.

## User Stories

### Epic 1: Smart Debugging & Logic Explanation

#### 1.1 Code Analysis and Error Detection
**As a** student with broken code  
**I want to** paste my C/Python code and get an intelligent analysis  
**So that** I can understand what went wrong beyond just syntax errors

**Acceptance Criteria:**
- System accepts C and Python code snippets up to 500 lines
- AI identifies logical errors, not just syntax issues
- Analysis completes within 10 seconds for typical code snippets
- System handles common student programming patterns (loops, conditionals, functions, pointers)

#### 1.2 Logic Gap Explanation
**As a** student who doesn't understand why my code failed  
**I want to** receive explanations in simple, non-technical English  
**So that** I can grasp the underlying programming concept I'm missing

**Acceptance Criteria:**
- Explanations use beginner-friendly language (avoid jargon)
- Each explanation includes the specific concept being violated
- Explanations are contextual to the student's code, not generic
- System provides before/after code examples when helpful

#### 1.3 Concept Identification and Correction Suggestions
**As a** student learning programming fundamentals  
**I want to** know which specific programming concept I need to review  
**So that** I can focus my study efforts effectively

**Acceptance Criteria:**
- System identifies specific concepts (e.g., "pointer dereferencing", "loop termination conditions")
- Provides corrected code snippet with highlighted changes
- Explains why the correction works
- Links correction to broader programming principles

### Epic 2: Viva Voce Preparation

#### 2.1 Interview Question Generation
**As a** student preparing for lab exams  
**I want to** receive potential viva questions based on my code  
**So that** I can practice explaining my logic and prepare for oral assessments

**Acceptance Criteria:**
- Generates exactly 3 questions per code snippet
- Questions focus on the logic and concepts used in the specific code
- Questions range from basic understanding to deeper conceptual knowledge
- Questions are appropriate for the complexity level of the submitted code

#### 2.2 Question Difficulty Scaling
**As a** student at different skill levels  
**I want to** receive questions appropriate to my code complexity  
**So that** I'm challenged appropriately without being overwhelmed

**Acceptance Criteria:**
- Basic code generates fundamental concept questions
- Intermediate code includes algorithm efficiency questions
- Advanced code includes design pattern and optimization questions
- System adapts question difficulty based on code sophistication

### Epic 3: Resource Discovery and Learning Path

#### 3.1 Targeted Resource Recommendations
**As a** student struggling with a specific concept  
**I want to** receive curated learning resources  
**So that** I can quickly find relevant documentation and tutorials

**Acceptance Criteria:**
- Recommends official documentation links for identified concepts
- Suggests specific video tutorial timestamps when available
- Provides multiple resource types (text, video, interactive)
- Resources are filtered for beginner-appropriate content

#### 3.2 Learning Path Guidance
**As a** student who wants to improve systematically  
**I want to** understand what concepts to learn next  
**So that** I can build knowledge progressively

**Acceptance Criteria:**
- Suggests prerequisite concepts if student lacks fundamentals
- Recommends next-level concepts after mastering current ones
- Provides estimated time investment for each learning path
- Tracks concept mastery over multiple sessions

### Epic 4: User Experience and Interface

#### 4.1 Intuitive Code Submission
**As a** student focused on learning  
**I want to** easily submit my code without complex setup  
**So that** I can get help quickly without technical barriers

**Acceptance Criteria:**
- Single-page interface with clear code input area
- Supports copy-paste and file upload
- Automatic language detection for C/Python
- Real-time character count and submission validation

#### 4.2 Clear Results Presentation
**As a** student receiving AI analysis  
**I want to** understand the results at a glance  
**So that** I can quickly identify what to focus on

**Acceptance Criteria:**
- Results organized in clear sections (Error, Explanation, Fix, Questions)
- Visual highlighting of problematic code sections
- Progressive disclosure of detailed information
- Mobile-responsive design for studying anywhere

### Epic 5: Learning Analytics and History

#### 5.1 Query History Tracking
**As a** student using CodeBuddy over time  
**I want to** see my previous submissions and progress  
**So that** I can track my learning journey and revisit concepts

**Acceptance Criteria:**
- Stores all submitted code snippets and analyses
- Provides searchable history by date, language, or concept
- Shows improvement trends over time
- Allows bookmarking of particularly helpful analyses

#### 5.2 Concept Mastery Tracking
**As a** student working on multiple programming concepts  
**I want to** see which areas I've mastered and which need work  
**So that** I can focus my study time effectively

**Acceptance Criteria:**
- Tracks frequency of errors by concept type
- Shows mastery progression for each programming concept
- Identifies recurring mistake patterns
- Provides personalized study recommendations

## Technical Requirements

### Performance Requirements
- **Response Time**: AI analysis completes within 10 seconds for 95% of requests
- **Availability**: 99.5% uptime during academic hours (8 AM - 10 PM local time)
- **Scalability**: Support 1000 concurrent users during peak usage
- **Code Size Limit**: Handle code snippets up to 500 lines efficiently

### Security Requirements
- **Data Privacy**: Student code is not stored permanently without explicit consent
- **API Security**: All AI service calls use encrypted connections
- **User Authentication**: Optional account creation for history tracking
- **Rate Limiting**: Prevent abuse with reasonable usage limits per user

### Integration Requirements
- **Amazon Bedrock**: Primary AI engine for logic analysis and explanation
- **Amazon Q**: Secondary AI for code suggestions and improvements
- **DynamoDB**: User session and history storage
- **External APIs**: Integration with documentation sources and video platforms

### Compatibility Requirements
- **Browsers**: Support Chrome, Firefox, Safari, Edge (latest 2 versions)
- **Languages**: Full support for C and Python syntax and semantics
- **Code Formats**: Accept plain text, common IDE exports, and file uploads
- **Mobile**: Responsive design for tablet and mobile usage

## Success Metrics

### Learning Effectiveness
- **Concept Understanding**: 80% of users report better understanding after using explanations
- **Error Reduction**: 60% reduction in similar errors in subsequent submissions
- **Viva Performance**: Students report improved confidence in oral assessments

### User Engagement
- **Session Duration**: Average session length of 15+ minutes
- **Return Usage**: 70% of users return within one week
- **Feature Adoption**: 80% of users try viva preparation mode

### Technical Performance
- **Response Accuracy**: 90% of AI explanations rated as helpful by users
- **System Reliability**: Less than 1% of requests result in errors
- **Resource Efficiency**: Average analysis cost under $0.05 per request

## Constraints and Assumptions

### Technical Constraints
- Must use Amazon Bedrock and Amazon Q as specified
- DynamoDB storage limitations for free tier users
- API rate limits from external documentation sources

### Business Constraints
- Development timeline aligned with hackathon schedule
- Budget constraints for AI service usage during development
- Compliance with educational institution data policies

### User Assumptions
- Students have basic familiarity with copying/pasting code
- Users have reliable internet connection for AI processing
- Students are motivated to understand concepts, not just get answers
- Academic institutions support AI-assisted learning tools

## Out of Scope (Future Versions)

- Support for languages other than C and Python
- Real-time collaborative debugging sessions
- Integration with specific IDE plugins
- Automated assignment grading capabilities
- Advanced plagiarism detection features
- Video call integration for live tutoring sessions