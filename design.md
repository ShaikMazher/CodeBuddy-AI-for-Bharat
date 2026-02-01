# CodeBuddy - AI Logic Tutor & Lab Assistant Design Document

## Design Philosophy

CodeBuddy is designed with two core principles that align with hackathon judging criteria:

1. **Clarity**: Every interaction should be immediately understandable to students at any programming level
2. **Usefulness**: Each feature directly addresses real pain points in programming education

## System Architecture

### High-Level Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   React.js      │    │   Python API     │    │   Amazon        │
│   Frontend      │◄──►│   (FastAPI)      │◄──►│   Bedrock       │
│                 │    │                  │    │   (Claude 3)    │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                │
                                ▼
                       ┌──────────────────┐    ┌─────────────────┐
                       │   DynamoDB       │    │   Amazon Q      │
                       │   (User Data)    │    │   (Code Assist) │
                       └──────────────────┘    └─────────────────┘
```

### Component Breakdown

#### Frontend Layer (React.js)
- **Code Input Component**: Clean interface for code submission
- **Analysis Display Component**: Structured presentation of AI results
- **Viva Questions Component**: Interactive Q&A preparation interface
- **History Dashboard**: User progress and session tracking
- **Resource Panel**: Curated learning materials display

#### Backend Layer (Python FastAPI)
- **Code Analysis Service**: Orchestrates AI analysis workflow
- **Bedrock Integration**: Handles Claude 3 Sonnet API calls
- **Amazon Q Integration**: Manages code suggestion requests
- **User Session Manager**: Tracks user interactions and history
- **Resource Aggregator**: Fetches and curates learning materials

#### Data Layer (DynamoDB)
- **User Sessions Table**: Stores user interactions and preferences
- **Code Analysis History**: Archives submitted code and AI responses
- **Concept Tracking Table**: Monitors user progress by programming concept
- **Resource Cache Table**: Caches frequently accessed learning materials

## User Experience Design

### User Flow Diagram

```
Start
  │
  ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Landing Page                                 │
│  "Paste your broken code and understand why it failed"         │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                   Code Input Interface                         │
│  ┌─────────────────┐  ┌──────────────┐  ┌─────────────────┐   │
│  │ Language Select │  │  Code Editor │  │  Submit Button  │   │
│  │ [C] [Python]    │  │  (Syntax     │  │  "Analyze Code" │   │
│  └─────────────────┘  │   Highlight) │  └─────────────────┘   │
│                       └──────────────┘                        │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                    AI Processing                                │
│              "Analyzing your code logic..."                     │
│                    [Progress Bar]                               │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Results Dashboard                            │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │   Error Found   │  │   Explanation   │  │  Corrected Code │ │
│  │ "Missing pointer│  │ "You forgot to  │  │  [Highlighted   │ │
│  │  dereference"   │  │  dereference..."│  │   Changes]      │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                   Viva Preparation Mode                         │
│  "Practice these questions for your lab exam:"                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Q1: What happens if you don't dereference this pointer? │   │
│  │ Q2: How would you debug this type of error?            │   │
│  │ Q3: What are the memory implications of this mistake?   │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Learning Resources                           │
│  "Learn more about this concept:"                              │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐ │
│  │   Documentation │  │   Video Tutorial│  │   Practice      │ │
│  │   "C Pointers   │  │   "Pointer Basics│  │   "Try these    │ │
│  │    Reference"   │  │    @12:30"      │  │    exercises"   │ │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘ │
└─────────────────────────┬───────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Session History                            │
│  "Your learning progress:"                                     │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Recent Sessions | Concept Mastery | Improvement Trends  │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

### Interface Design Principles

#### Clarity-Focused Design
1. **Single-Purpose Screens**: Each screen has one primary function
2. **Progressive Disclosure**: Advanced features revealed as needed
3. **Visual Hierarchy**: Important information prominently displayed
4. **Consistent Language**: Technical terms explained in context

#### Usefulness-Focused Features
1. **Immediate Value**: Results visible within 10 seconds
2. **Actionable Insights**: Every analysis includes next steps
3. **Contextual Help**: Resources matched to specific problems
4. **Progress Tracking**: Visible improvement over time

## AI Integration Design

### Amazon Bedrock (Claude 3 Sonnet) Integration

#### Primary Use Cases
1. **Logic Analysis**: Deep understanding of code semantics and intent
2. **Error Explanation**: Natural language description of programming mistakes
3. **Concept Identification**: Mapping errors to fundamental programming concepts
4. **Viva Question Generation**: Creating contextual interview questions

#### Prompt Engineering Strategy

```python
# Example prompt structure for logic analysis
ANALYSIS_PROMPT = """
You are an expert programming tutor helping a student understand their code.

Student's Code:
{code}

Language: {language}

Task: Analyze this code and provide:
1. Primary logical error (not syntax)
2. Simple explanation suitable for a beginner
3. The programming concept they need to understand
4. Corrected version with minimal changes

Focus on learning, not just fixing. Explain WHY the error occurred.
"""

VIVA_PROMPT = """
Based on this code analysis, generate exactly 3 viva voce questions:

Code Context: {code}
Error Found: {error}
Concept: {concept}

Generate questions that:
1. Test basic understanding of the concept
2. Explore practical application
3. Challenge deeper comprehension

Questions should be appropriate for a student lab exam.
"""
```

### Amazon Q Integration

#### Secondary Use Cases
1. **Code Suggestions**: Alternative implementations
2. **Best Practices**: Industry-standard coding patterns
3. **Optimization Hints**: Performance improvement suggestions
4. **Documentation Links**: Official reference materials

### AI Response Processing Pipeline

```
Raw Code Input
      │
      ▼
┌─────────────────┐
│ Preprocessing   │ ← Language detection, syntax validation
└─────────┬───────┘
          │
          ▼
┌─────────────────┐
│ Bedrock Analysis│ ← Primary logic analysis
└─────────┬───────┘
          │
          ▼
┌─────────────────┐
│ Amazon Q Query  │ ← Code suggestions and resources
└─────────┬───────┘
          │
          ▼
┌─────────────────┐
│ Response Fusion │ ← Combine and structure results
└─────────┬───────┘
          │
          ▼
┌─────────────────┐
│ User Interface  │ ← Present to student
└─────────────────┘
```

## Data Model Design

### DynamoDB Table Structures

#### User Sessions Table
```json
{
  "PK": "USER#session_id",
  "SK": "SESSION#timestamp",
  "user_id": "optional_user_identifier",
  "session_start": "2024-01-15T10:30:00Z",
  "session_end": "2024-01-15T10:45:00Z",
  "total_queries": 3,
  "languages_used": ["python", "c"],
  "concepts_covered": ["loops", "pointers"]
}
```

#### Code Analysis History Table
```json
{
  "PK": "ANALYSIS#analysis_id",
  "SK": "CODE#timestamp",
  "session_id": "session_reference",
  "original_code": "student_submitted_code",
  "language": "python",
  "error_type": "logic_error",
  "concept_identified": "loop_termination",
  "ai_explanation": "detailed_explanation_text",
  "corrected_code": "fixed_version",
  "viva_questions": ["q1", "q2", "q3"],
  "resources_suggested": ["doc_link1", "video_link2"],
  "processing_time_ms": 8500
}
```

#### Concept Mastery Tracking Table
```json
{
  "PK": "USER#user_id",
  "SK": "CONCEPT#concept_name",
  "concept": "pointer_dereferencing",
  "first_encounter": "2024-01-10T09:00:00Z",
  "last_encounter": "2024-01-15T10:30:00Z",
  "total_errors": 5,
  "recent_errors": 1,
  "mastery_level": "improving",
  "success_rate": 0.8
}
```

## API Design

### RESTful Endpoints

#### Core Analysis Endpoint
```http
POST /api/v1/analyze
Content-Type: application/json

{
  "code": "string",
  "language": "c|python",
  "session_id": "optional_string"
}

Response:
{
  "analysis_id": "unique_identifier",
  "error_detected": true,
  "error_type": "logic_error",
  "concept": "pointer_dereferencing",
  "explanation": "You forgot to dereference the pointer...",
  "corrected_code": "fixed_version_with_highlights",
  "viva_questions": [
    "What happens when you don't dereference a pointer?",
    "How do you debug pointer-related errors?",
    "What are the memory safety implications?"
  ],
  "resources": [
    {
      "type": "documentation",
      "title": "C Pointers Reference",
      "url": "https://docs.example.com/c-pointers"
    }
  ],
  "processing_time_ms": 8500
}
```

#### Session History Endpoint
```http
GET /api/v1/history/{session_id}

Response:
{
  "session_id": "identifier",
  "analyses": [
    {
      "timestamp": "2024-01-15T10:30:00Z",
      "language": "python",
      "concept": "loop_logic",
      "success": true
    }
  ],
  "concept_progress": {
    "mastered": ["variables", "conditionals"],
    "improving": ["loops"],
    "needs_work": ["pointers"]
  }
}
```

## Security and Privacy Design

### Data Protection Strategy
1. **Code Privacy**: Student code not permanently stored without consent
2. **Session Isolation**: Each session cryptographically isolated
3. **API Security**: Rate limiting and input validation on all endpoints
4. **AI Service Security**: Encrypted communication with AWS services

### Privacy-First Features
1. **Anonymous Mode**: Full functionality without account creation
2. **Data Retention Control**: User-controlled history deletion
3. **Minimal Data Collection**: Only essential information stored
4. **Transparent Processing**: Clear explanation of how code is analyzed

## Performance and Scalability Design

### Response Time Optimization
1. **Parallel Processing**: Bedrock and Amazon Q queries run concurrently
2. **Intelligent Caching**: Common error patterns cached for instant response
3. **Progressive Loading**: UI updates as analysis components complete
4. **Timeout Handling**: Graceful degradation if AI services are slow

### Scalability Architecture
1. **Stateless API**: Horizontal scaling of backend services
2. **CDN Integration**: Static assets served from edge locations
3. **Database Optimization**: DynamoDB auto-scaling for traffic spikes
4. **Load Balancing**: Multiple API instances behind load balancer

## Testing Strategy

### Correctness Properties for Property-Based Testing

#### 1. Analysis Consistency Property
**Property**: For identical code inputs, the system should produce consistent error identification and concept mapping.

**Test Strategy**: Generate variations of the same logical error across different variable names and contexts. Verify that the core concept identification remains stable.

#### 2. Explanation Clarity Property
**Property**: All AI-generated explanations should be understandable to students at the target skill level.

**Test Strategy**: Use readability metrics and keyword complexity analysis to ensure explanations meet beginner-friendly criteria.

#### 3. Viva Question Relevance Property
**Property**: Generated viva questions should directly relate to the concepts identified in the code analysis.

**Test Strategy**: Verify semantic similarity between identified concepts and question topics using NLP similarity measures.

#### 4. Resource Recommendation Accuracy Property
**Property**: Suggested learning resources should match the specific programming concept identified in the analysis.

**Test Strategy**: Validate that recommended documentation and tutorials contain the identified concept keywords and are appropriate for the skill level.

#### 5. Response Time Consistency Property
**Property**: System response time should remain under 10 seconds for 95% of typical code submissions.

**Test Strategy**: Generate code samples of varying complexity and measure end-to-end response times under different load conditions.

### Unit Testing Framework
- **Frontend**: Jest + React Testing Library
- **Backend**: pytest with FastAPI test client
- **Integration**: End-to-end tests with Playwright
- **Property-Based Testing**: Hypothesis (Python) for backend, fast-check (JavaScript) for frontend

## Deployment and Infrastructure

### AWS Infrastructure Design
1. **Compute**: ECS Fargate for containerized API services
2. **Storage**: DynamoDB for user data, S3 for static assets
3. **AI Services**: Bedrock and Amazon Q with appropriate IAM roles
4. **Networking**: CloudFront CDN with Route 53 DNS
5. **Monitoring**: CloudWatch for metrics and logging

### Development Environment
1. **Local Development**: Docker Compose for full stack
2. **CI/CD Pipeline**: GitHub Actions with AWS deployment
3. **Environment Management**: Separate dev/staging/prod configurations
4. **Secret Management**: AWS Secrets Manager for API keys

## Success Metrics and Analytics

### Learning Effectiveness Metrics
1. **Concept Understanding Rate**: Percentage of users who report improved understanding
2. **Error Reduction Tracking**: Decrease in similar errors over time
3. **Viva Preparation Success**: User confidence ratings for oral assessments

### Technical Performance Metrics
1. **Response Accuracy**: AI explanation helpfulness ratings
2. **System Reliability**: Uptime and error rate monitoring
3. **User Engagement**: Session duration and return visit rates

### Business Impact Metrics
1. **User Adoption**: New user registration and retention rates
2. **Feature Utilization**: Usage patterns across different features
3. **Educational Outcomes**: Correlation with improved academic performance

## Future Enhancement Roadmap

### Phase 2 Features
1. **Multi-Language Support**: Java, JavaScript, and other languages
2. **Collaborative Features**: Peer code review and discussion
3. **Advanced Analytics**: Detailed learning path recommendations
4. **Mobile App**: Native iOS and Android applications

### Phase 3 Features
1. **IDE Integration**: Plugins for popular development environments
2. **Real-time Assistance**: Live coding help and suggestions
3. **Instructor Dashboard**: Tools for educators to track student progress
4. **Gamification**: Achievement system and learning challenges

This design document provides a comprehensive blueprint for building CodeBuddy with emphasis on clarity and usefulness, ensuring it meets the hackathon judging criteria while delivering genuine value to programming students.