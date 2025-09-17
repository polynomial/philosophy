# Chapter 8: Power Structures in the Repository: Politics of the Pull Request

> "Power is not an institution, and not a structure; neither is it a certain strength we are endowed with; it is the name that one attributes to a complex strategical situation in a particular society." — Michel Foucault¹

> "The history of all hitherto existing society is the history of class struggles." — Karl Marx²

> "With great power comes great responsibility." — Uncle Ben (also applicable to sudo and admin rights)³

## The Repository as Political Space

Every repository is a microcosm of political structure. From the moment `git init` creates that `.git` directory, a space of power relations is born. Who can commit? Who can merge? Who decides the architecture? Who gets credited? These aren't just technical questions—they're fundamentally political ones.

The repository, like any political space, features:
- **Territory** (code ownership)
- **Hierarchy** (maintainer/contributor roles)
- **Law** (coding standards, CI/CD rules)
- **Economics** (attention, time, recognition)
- **Conflict** (competing visions, approaches)
- **Revolution** (forks, rewrites)

Let's examine how power flows through our digital dominions.

## The Architecture of Control

### CODEOWNERS: Digital Feudalism

The `CODEOWNERS` file is a fascinating artifact of power distribution:

```
# CODEOWNERS - Mapping territory to lords

# The Database Duchy
/src/database/ @db-team

# The Frontend Fiefdom  
/src/ui/ @ui-team @sarah @john

# The Authentication Absolutism
/src/auth/ @security-team

# The Commons (anyone can review)
/docs/ @everyone
/tests/integration/ @qa-team @dev-team
```

This isn't just about efficient code review routing. It's about:
- **Territorial Control**: "This is our domain"
- **Gatekeeping**: "Changes must pass through us"
- **Expertise Recognition**: "We are the authorities here"
- **Responsibility Assignment**: "We own the consequences"

The parallel to feudalism is striking. Like medieval lords granted dominion over lands, code owners are granted dominion over directories⁴. They extract "rent" in the form of review time and hold the power to accept or reject changes to "their" code.

### Branch Protection: The Constitution

Branch protection rules function as a repository's constitution:

```yaml
# .github/branch-protection.yml
protection_rules:
  master:
    required_reviews: 2
    dismiss_stale_reviews: true
    require_code_owner_reviews: true
    required_status_checks:
      - continuous-integration/travis-ci
      - codecov/patch
    enforce_admins: true
    restrictions:
      users: ["release-bot"]
      teams: ["senior-developers"]
```

These rules encode power structures:
- **Checks and Balances**: Multiple reviewers prevent autocracy
- **Due Process**: CI must pass before merge
- **Term Limits**: Stale reviews are dismissed
- **Constitutional Amendments**: Only certain users can override

But like any constitution, these rules can be suspended by those with sufficient power—repository admins can force-push, bypass protections, rewrite history⁵.

### The CI/CD Pipeline as Panopticon

Foucault's concept of the panopticon—a prison where all inmates might be watched at any time—finds digital expression in CI/CD⁶:

```yaml
# .github/workflows/all-seeing-eye.yml
name: Continuous Surveillance
on: [push, pull_request]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Check code style
      - name: Enforce conventions
      
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Run unit tests
      - name: Check coverage
      
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Scan for vulnerabilities
      - name: Check dependencies
```

The pipeline watches everything:
- Every push is scrutinized
- Every PR is judged
- Every deviation is flagged
- Every developer internalizes the rules

The brilliance of the panopticon is that it doesn't need to watch all the time—the possibility of being watched changes behavior. Developers run tests locally, fix linting errors preemptively, self-censor commits. The CI/CD pipeline achieves disciplinary power through architecture⁷.

## The Political Economy of Open Source

### The Maintainer's Burden

In open source, maintainers wield enormous power but at enormous cost:

```javascript
class OpenSourceMaintainer {
  constructor() {
    this.power = {
      mergeAuthority: true,
      designDecisions: true,
      communityDirection: true
    };
    
    this.burden = {
      unpaidLabor: Infinity,
      emotionalLabor: "constant",
      burnoutRisk: "high",
      thanklessWork: true
    };
  }
  
  handlePullRequest(pr) {
    // Every PR is a political decision
    if (this.alignsWithVision(pr) && 
        this.maintainsQuality(pr) &&
        this.hasEnergyToReview(pr)) {
      return this.merge(pr);
    }
    // The power to say no is the heaviest burden
    return this.explainRejection(pr);
  }
}
```

The maintainer paradox: they have autocratic power over the project but are servants to the community. They can make any technical decision but must manage endless social dynamics. They own everything and nothing⁸.

### The Contributor's Gambit

Contributors navigate complex power dynamics:

```markdown
## First Contribution - The Supplicant Approach

Hello! First-time contributor here 👋

I noticed [small issue] and thought I could help. This PR:
- Fixes the specific issue
- Includes tests
- Follows your contribution guidelines
- Doesn't change anything else

I'm happy to make any changes you suggest!

[Excessive deference to establish harmlessness]
```

versus:

```markdown
## Experienced Contributor - The Peer Approach

This implements the feature discussed in #1234.

Changes:
- Added new API endpoint
- Refactored authentication flow
- Updated documentation

Breaking changes are documented in CHANGELOG.

[Assumes competence and equality]
```

The tone shifts with perceived power. New contributors must prove they're not threats to the project's stability. Established contributors can assume their changes will be taken seriously⁹.

### The Fork as Revolution

The ultimate check on maintainer power is the fork:

```bash
# The revolutionary act
git clone https://github.com/original/project
cd project
git remote rename origin upstream
git remote add origin https://github.com/revolutionary/project
git push origin master

# The declaration of independence
echo "This project has been forked due to [grievances]" > README.md
```

Forking is the "right of revolution" in open source. When governance fails, when maintainers become tyrants, when the community's needs diverge from leadership's vision—forking provides an escape valve¹⁰.

Famous forks tell political stories:
- **Node.js → io.js**: Governance dispute (later reunified)
- **MySQL → MariaDB**: Corporate acquisition fears
- **OpenOffice → LibreOffice**: Oracle's stewardship concerns
- **Bitcoin → Bitcoin Cash**: Philosophical differences on scaling

Each fork is a political schism made manifest in code¹¹.

## The Microaggressions of Code Review

### The Tone Police

Power in code review often manifests through tone:

```markdown
# The Dismissive Review
"This is wrong. Read the docs."

# The Condescending Review
"I guess you didn't understand how this works. Let me explain..."

# The Gatekeeping Review
"We don't do things that way here."

# The Bikeshedding Review
"I won't approve until you rename this variable."
```

versus:

```markdown
# The Constructive Review
"I see what you're trying to do. Have you considered X? 
It might handle edge case Y better."

# The Educational Review
"This works! For future reference, pattern X can help with this."

# The Collaborative Review
"What if we tried approach X? What do you think?"
```

The difference isn't just kindness—it's about power dynamics. Dismissive reviews assert dominance. Constructive reviews share power¹².

### The Architecture Astronaut's Veto

Those with architectural authority wield special power:

```java
// The simple solution that works
public class UserService {
    public User getUser(String id) {
        return database.findUser(id);
    }
}

// The architect's demand
public class UserService implements IUserService {
    private final IUserRepository repository;
    private final ICacheManager cache;
    private final IEventBus eventBus;
    private final IMetricsCollector metrics;
    
    @Inject
    public UserService(IUserRepository repository, 
                      ICacheManager cache,
                      IEventBus eventBus, 
                      IMetricsCollector metrics) {
        // ... 50 lines of initialization
    }
    
    @Override
    @Transactional
    @Cacheable
    @Metrics("user.get")
    public User getUser(String id) {
        // ... 30 lines of orchestration
    }
}
```

"But it needs to be extensible!" becomes a power play. The ability to demand complexity, to insist on abstractions, to require "enterprise patterns"—this is architectural power unchecked¹³.

## The Gender and Diversity Dynamics

### The Old Boys' Club

Despite efforts to improve, tech often functions as an old boys' club:

```python
# The subtle exclusions
def get_conference_speakers():
    speakers = []
    # "We only invited people we know"
    for contact in personal_network:
        if contact.is_visible and contact.speaks_english:
            speakers.append(contact)
    return speakers  # Mysteriously homogeneous

# The not-so-subtle exclusions
def evaluate_candidate():
    # "Culture fit" as exclusion mechanism
    if candidate.went_to_same_schools or \
       candidate.shares_hobbies or \
       candidate.reminds_me_of_myself:
        return "good culture fit"
    return "not a culture fit"
```

Power perpetuates itself through networks, "culture fit," and unconscious bias¹⁴.

### The Emotional Labor Tax

Underrepresented developers often pay an emotional labor tax:

```javascript
class UnderrepresentedDeveloper extends Developer {
  constructor() {
    super();
    this.additionalResponsibilities = [
      "Educate others about diversity",
      "Represent entire demographic",
      "Handle inappropriate comments gracefully",
      "Prove competence repeatedly",
      "Navigate hostile environments",
      "Mentor other underrepresented folks"
    ];
  }
  
  contributeCode() {
    // Same work...
    super.contributeCode();
    // ...plus invisible emotional labor
    this.handleMicroaggressions();
    this.educateWellMeaningColleagues();
    this.proveCompetenceAgain();
  }
}
```

This invisible work is rarely recognized, never compensated, but constantly expected¹⁵.

## The Temporal Politics of Development

### Synchronous Privilege

Power accrues to those who can participate synchronously:

```yaml
# Meeting-driven decisions favor:
- People in company time zones
- People without caregiving responsibilities  
- People with flexible schedules
- People comfortable speaking in meetings

# Asynchronous communication democratizes:
- Global participation
- Thoughtful written responses
- Documentation of decisions
- Time for non-native speakers
```

The choice between synchronous and asynchronous collaboration is a political choice about who gets to participate¹⁶.

### The Speed of Merge

The speed at which PRs are reviewed and merged reflects power:

```python
def get_merge_time(pr):
    if pr.author in core_team:
        return "hours"
    elif pr.author in trusted_contributors:
        return "days"
    elif pr.author in first_time_contributors:
        return "weeks"
    elif pr.author in blacklisted_users:
        return "never"
```

This isn't always malicious—core team members have established trust, their changes are often critical. But it creates a hierarchy where some contributors are more equal than others¹⁷.

## The Violence of the Rewrite

### Creative Destruction

The decision to rewrite is an act of violence against existing code:

```bash
# The revolutionary's manifesto
rm -rf legacy_system/
mkdir clean_slate/
echo "Starting fresh with modern patterns" > README.md

# What's destroyed:
# - Years of bug fixes
# - Accumulated domain knowledge
# - Working solutions to edge cases
# - The labor of previous developers
```

Rewrites are often power plays by new technical leadership, assertions that the old guard's work was fundamentally flawed. They're technical coups that erase history¹⁸.

### The Preservationist's Resistance

Those who maintain legacy systems often lack power:

```java
// The maintainer's lament
public class LegacySystem {
    // "Don't touch this, it works"
    // "We don't know why this is here but removing it breaks prod"
    // "TODO: Refactor this (added 2008-03-15)"
    
    @Deprecated // But still essential
    public void criticalBusinessLogic() {
        // 500 lines of accumulated wisdom
        // Every line is there for a reason
        // Every reason is a production incident
    }
}
```

Maintaining isn't as glamorous as creating. Those who keep the lights on rarely get the recognition (or power) of those who build new things¹⁹.

## The Surveillance Capitalism of Code

### The Metrics That Matter

What we measure reflects what we value, and what we value reflects power:

```sql
-- The individual performance query
SELECT 
    developer,
    COUNT(*) as commits,
    SUM(additions) - SUM(deletions) as loc_contributed,
    COUNT(DISTINCT pull_requests) as prs_merged
FROM github_stats
GROUP BY developer
ORDER BY commits DESC;

-- What this misses:
-- Code reviews given
-- Mentoring provided
-- Documentation written
-- Bugs prevented
-- Team morale improved
```

Metrics become tools of power—those who define what's measured define what's valued²⁰.

### The Reputation Economy

GitHub profiles function as developer credit scores:

```javascript
class GitHubProfile {
    calculateReputation() {
        return {
            stars: this.totalStarsReceived,
            followers: this.followerCount,
            contributions: this.contributionGraph,
            // The invisible labor
            issuesHelped: undefined,
            questionsAnswered: undefined,
            newcomersWelcomed: undefined,
            toxicityPrevented: undefined
        };
    }
}
```

This reputation economy advantages those who:
- Work on popular projects
- Have time for open source
- Self-promote effectively
- Write in English
- Live in GitHub-friendly time zones²¹

## Resistance and Subversion

### The Malicious Compliance

Developers resist power through malicious compliance:

```python
# The letter of the law
def follow_arbitrary_rule():
    """
    Management wants all functions documented.
    This is documentation.
    It documents that this function exists.
    It has parameters (sometimes).
    It returns something (or not).
    Happy now?
    """
    pass

# The 100% test coverage mandate
def test_trivial_getter():
    """Testing getters because coverage metrics"""
    assert object.get_value() == object.value
```

By following rules to absurd conclusions, developers highlight their arbitrariness²².

### The Shadow IT

When official channels fail, shadow systems emerge:

```bash
# The unofficial tools
alias deploy="echo 'Using official process' && ./secret_fast_deploy.sh"
alias test="./skip_flaky_tests.sh && ./actual_tests.sh"

# The real documentation
# wiki.internal.com → "Official docs"
# real-docs.slack.com → Where answers actually live
```

Shadow IT represents bottom-up resistance to top-down power structures²³.

## Building Better Power Structures

### The Benevolent Dictator Model

Some projects thrive under benevolent dictators:

```python
class BenevolentDictator:
    def __init__(self):
        self.power = "absolute"
        self.responsibility = "total"
        self.vision = "clear"
        
    def decide(self, issue):
        community_input = self.gather_feedback(issue)
        decision = self.make_call(community_input)
        self.explain_reasoning(decision)
        return self.implement_decisively(decision)
```

When it works: Clear vision, fast decisions, coherent design (Linux, Python)
When it fails: Burnout, blind spots, succession crises²⁴

### The Federation Model

Some projects distribute power through federation:

```yaml
# Rust's governance
teams:
  core:
    responsibility: "Overall direction"
    members: ["rotating", "elected"]
  
  language:
    responsibility: "Language evolution"
    autonomy: "high"
    
  compiler:
    responsibility: "Implementation"
    autonomy: "high"
    
  community:
    responsibility: "Code of conduct, events"
    autonomy: "high"
```

Power is divided by domain, decisions are made by those with relevant expertise²⁵.

### The Anarchist Collective

Some projects attempt to eliminate hierarchy entirely:

```javascript
// The collective model
function makeDecision(proposal) {
    const discussion = openDiscussion(proposal);
    const consensus = seekConsensus(discussion);
    
    if (consensus.isReached()) {
        return implement(consensus);
    } else {
        return iterateProposal(proposal, discussion);
    }
}

// No single merger, no fixed leaders
// Slow but inclusive
```

This works for small, aligned groups but struggles to scale²⁶.

## Conclusion: Code as Politics By Other Means

Clausewitz said war is politics by other means. In software, code is politics by other means. Every technical decision encodes power relations. Every process embodies political philosophy. Every tool enables certain structures while preventing others.

We cannot escape politics in programming because we cannot escape power. The moment two people collaborate on code, power dynamics emerge:
- Who decides the architecture?
- Whose code style prevails?
- Who gets credit?
- Who maintains?
- Who benefits?

Recognizing these power structures is the first step toward improving them. We can choose:
- Autocracy or democracy
- Hierarchy or flatness
- Exclusion or inclusion
- Competition or collaboration

But we cannot choose to have no politics. The only choice is whether to acknowledge the politics we have and work to improve them, or pretend they don't exist and let them fester in darkness.

The next time you review a PR, consider: what power dynamics are at play? The next time you design a process, ask: who does this empower or disempower? The next time you contribute to a project, observe: how does power flow?

Because in the end, we're not just building software. We're building the social structures within which software gets built. And those structures matter as much as any algorithm or architecture.

The repository is a body politic. The question is: what kind of politics will we practice?

---

## References and Further Reading

1. Foucault, M. (1982). "The Subject and Power". Critical Inquiry, 8(4), 777-795.
2. Marx, K. & Engels, F. (1848). *The Communist Manifesto*. London.
3. Lee, S. & Ditko, S. (1962). Amazing Fantasy #15. Marvel Comics.
4. Weber, M. (1946). "Politics as a Vocation". In *From Max Weber*. Oxford University Press.
5. Torvalds, L. (2000). Linux Kernel Mailing List archives. lkml.org
6. Foucault, M. (1975). *Discipline and Punish*. Paris: Gallimard.
7. Bentham, J. (1791). *Panopticon; or, The Inspection-House*. London.
8. Eghbal, N. (2020). *Working in Public: The Making and Maintenance of Open Source Software*. Stripe Press.
9. Raymond, E.S. (2001). *The Cathedral and the Bazaar*. O'Reilly Media.
10. Stallman, R. (2002). *Free Software, Free Society*. GNU Press.
11. Fogel, K. (2005). *Producing Open Source Software*. O'Reilly Media.
12. Freeman, J. (1972). "The Tyranny of Structurelessness". Berkeley Journal of Sociology.
13. Brooks, F. (1975). *The Mythical Man-Month*. Addison-Wesley.
14. Nafus, D. (2012). "'Patches don't have gender': What is not open in open source software". New Media & Society, 14(4).
15. Hochschild, A.R. (1983). *The Managed Heart*. University of California Press.
16. Herbsleb, J.D. & Mockus, A. (2003). "An empirical study of speed and communication in globally distributed software development". IEEE TSE, 29(6).
17. Bourdieu, P. (1986). "The Forms of Capital". In *Handbook of Theory and Research for the Sociology of Education*.
18. Spolsky, J. (2000). "Things You Should Never Do, Part I". Joel on Software.
19. Vinsel, L. & Russell, A.L. (2020). *The Innovation Delusion*. Currency.
20. Muller, J.Z. (2018). *The Tyranny of Metrics*. Princeton University Press.
21. Marlow, J., et al. (2013). "Impression formation in online peer production". CHI '13.
22. Scott, J.C. (1985). *Weapons of the Weak*. Yale University Press.
23. Behrens, S. (2009). "Shadow systems: the good, the bad and the ugly". Communications of the ACM, 52(2).
24. Raymond, E.S. (1999). "The Cathedral and the Bazaar". O'Reilly Media.
25. Rust Governance. (2021). "Rust Governance Structure". rust-lang.org
26. Freeman, J. (1972). "The Tyranny of Structurelessness". Berkeley Journal of Sociology.

## Questions for Reflection

1. What power structures exist in your current project? Are they explicit or implicit?

2. Have you experienced or witnessed power dynamics affecting technical decisions?

3. How does your organization measure developer productivity? What behaviors does this incentivize?

4. What invisible labor do you perform that isn't recognized or valued?

5. How could the power structures in your team or project be more equitable?

## Practical Exercises

1. **Power Mapping**: Map the actual power structure of your project (not the org chart). Who really makes decisions?

2. **Review Analysis**: Analyze your last 10 code reviews. What power dynamics were at play? How could they be improved?

3. **Metric Design**: Design metrics that would value collaboration, mentoring, and maintenance, not just feature delivery.

4. **Fork Study**: Study a major open source fork. What power dynamics led to the split? How did each project evolve?

5. **Process Audit**: Examine your team's processes. Who do they empower? Who might they exclude?

---

*Next Chapter: [The Myth of the 10x Developer: Excellence, Elitism, and Ego](./09_myth_of_10x.md)*
