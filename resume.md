---
layout: page
title: Resume
permalink: /resume/
order: 2
---

<style>
    .post-title { display: none !important; }
    
    .resume-wrapper {
        max-width: 800px;
        margin: 0 auto;
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        color: #333;
        line-height: 1.5;
        padding-bottom: 3rem;
    }

    .resume-header {
        text-align: center;
        margin-bottom: 2rem;
        border-bottom: 2px solid #333;
        padding-bottom: 1rem;
    }

    .resume-name {
        font-size: 2.2rem;
        font-weight: 700;
        text-transform: uppercase;
        letter-spacing: 1px;
        margin-bottom: 0.5rem;
    }

    .resume-section {
        margin-bottom: 1.5rem;
    }

    .section-title {
        font-size: 1.1rem;
        font-weight: 700;
        text-transform: uppercase;
        border-bottom: 1px solid #ccc;
        margin-bottom: 1rem;
        padding-bottom: 0.2rem;
    }

    .resume-item {
        margin-bottom: 1rem;
    }

    .item-header {
        display: flex;
        justify-content: space-between;
        align-items: baseline;
        flex-wrap: wrap;
    }

    .item-title {
        font-weight: 700;
        font-size: 1rem;
    }

    .item-subtitle {
        font-style: italic;
    }
    
    .item-date {
        font-style: italic;
        white-space: nowrap;
    }
    
    .item-location {
        font-style: italic;
    }

    .item-details ul {
        margin: 0.5rem 0 0 1.2rem;
        padding: 0;
        list-style-type: disc;
    }

    .item-details li {
        margin-bottom: 0.3rem;
        font-size: 0.95rem;
    }

    .skills-list p {
        margin: 0.3rem 0;
        font-size: 0.95rem;
    }

    .skills-label {
        font-weight: 700;
    }
    
    @media (max-width: 600px) {
        .item-header {
            flex-direction: column;
        }
        .item-date {
            margin-top: 0.2rem;
        }
    }
</style>

<div class="resume-wrapper">
    <header class="resume-header">
        <h1 class="resume-name">Niki Karanikola</h1>
    </header>

    <section class="resume-section">
        <h2 class="section-title">Education</h2>
        
        <div class="resume-item">
            <div class="item-header">
                <div>
                    <span class="item-title">Cornell Tech, Cornell University</span>
                    <span class="item-location">New York, NY</span>
                </div>
                <span class="item-date">May 2027</span>
            </div>
            <div class="item-subtitle">MS in Applied Info Science & Info Systems – Connective Media</div>
            <div class="item-details">
                <p style="margin: 0.2rem 0; font-size: 0.9rem;">Relevant Coursework: Algorithms and Data Structures, ML Engineering, Applied ML, Deep Learning</p>
            </div>
        </div>

        <div class="resume-item">
            <div class="item-header">
                <div>
                    <span class="item-title">Bennington College</span>
                    <span class="item-location">Bennington, VT</span>
                </div>
                <span class="item-date">May 2023</span>
            </div>
            <div class="item-subtitle">BS in Computer Science, GPA: 3.88</div>
            <div class="item-details">
                <p style="margin: 0.2rem 0; font-size: 0.9rem;">Relevant Coursework: Algorithms and Data Structures, Object Oriented Programming, Data Engineering</p>
            </div>
        </div>
    </section>

    <section class="resume-section">
        <h2 class="section-title">Technical Skills</h2>
        <div class="skills-list">
            <p><span class="skills-label">Coding Languages:</span> Python, SQL, Java, C++, CSS, HTML, JavaScript</p>
            <p><span class="skills-label">ML Tools:</span> Pandas, NumPy, scikit-learn, TensorFlow, keras, SciPy, HuggingFace, xgboost, lightgbm, nltk, plotly, matplotlib, seaborn</p>
            <p><span class="skills-label">Other Tools:</span> Git, Docker, GCP, AWS, Terraform, Spark, Linux</p>
        </div>
    </section>

    <section class="resume-section">
        <h2 class="section-title">Professional Experience</h2>

        <div class="resume-item">
            <div class="item-header">
                <div>
                    <span class="item-title">Veolia North America</span>
                    <span class="item-subtitle">Machine Learning Engineer</span>
                </div>
                <span class="item-date">Aug 2023 – June 2025</span>
            </div>
            <div class="item-location">New York, NY</div>
            <div class="item-details">
                <ul>
                    <li>Developed a RAG application using GPT-4, Langchain, and GCP Vector Search to generate SQL code from natural language, reducing data access time from weeks to minutes</li>
                    <li>Engineered a scalable LLM application with Gemini 2.0 Flash, Google Search tool, and Langchain to automate the generation of 18 competitor reports, delivering insights to sales and executives, increasing reporting frequency from biannual to monthly</li>
                    <li>Integrated Cohere reranking algorithm to an internal information retrieval system, increasing context relevance by 20%</li>
                    <li>Deployed infrastructure pipeline using Cloud Run, App Engine, Cloud Load Balancing, and Cloud DNS in GCP, enabling CI/CD</li>
                    <li>Built a predictive models using sklearn to codify tribal knowledge, enabling novice operators to optimize facilities</li>
                </ul>
            </div>
        </div>

        <div class="resume-item">
            <div class="item-header">
                <div>
                    <span class="item-title">Veolia North America</span>
                    <span class="item-subtitle">Data Science Intern</span>
                </div>
                <span class="item-date">Feb 2023 – May 2023</span>
            </div>
            <div class="item-location">Boston, MA</div>
            <div class="item-details">
                <ul>
                    <li>Improved a client acquisition model’s f1 score to ~90% by applying feature engineering and feature selection methods, ~40% improvement over the baseline</li>
                    <li>Deployed an API endpoint on Google Cloud Run to deliver real-time model predictions to Salesforce.</li>
                    <li>Communicated technical solution to non-technical leadership using visualizations created with plotly and seaborn.</li>
                </ul>
            </div>
        </div>

        <div class="resume-item">
            <div class="item-header">
                <div>
                    <span class="item-title">Massachusetts Institute of Technology Data + Feminism Lab</span>
                    <span class="item-subtitle">ML Researcher</span>
                </div>
                <span class="item-date">Sep 2022 – May 2023</span>
            </div>
            <div class="item-location">Cambridge, MA</div>
            <div class="item-details">
                <ul>
                    <li>Reduced the training dataset’s size by 30% while maintaining high model performance with active learning sampling.</li>
                    <li>Conducted and evaluated research findings using experimental design across 4 datasets and 4 metrics</li>
                    <li>Presented research findings at the ACM conference (70+ attendees) at Smith College and authored a Medium publication</li>
                </ul>
            </div>
        </div>

        <div class="resume-item">
            <div class="item-header">
                <div>
                    <span class="item-title">3Degrees Inc.</span>
                    <span class="item-subtitle">Full Stack Developer Intern</span>
                </div>
                <span class="item-date">Jun 2022 – Sep 2022</span>
            </div>
            <div class="item-location">San Francisco, CA</div>
            <div class="item-details">
                <ul>
                    <li>Developed web app using React, JavaScript, CSS, and Node.js to catalog price data for the sales team</li>
                    <li>Translated insights from 50+ stakeholder interviews into user-friendly wireframes in Figma, improving the user experience</li>
                </ul>
            </div>
        </div>
    </section>

    <section class="resume-section">
        <h2 class="section-title">Projects</h2>

        <div class="resume-item">
            <div class="item-header">
                <span class="item-title">CarePilot (Python)</span>
                <span class="item-date">Nov 2025</span>
            </div>
            <div class="item-details">
                <p style="margin-bottom: 0.3rem; font-style: italic;">Built an all in one platform to understand our health easier at the K2 Think Hackathon (top 16 finalist out of 900).</p>
                <ul>
                    <li>Created a 4-agent system using k2-think and CoT prompting to analyze lab data, insurance benefits, and generate claim appeals.</li>
                </ul>
            </div>
        </div>

        <div class="resume-item">
            <div class="item-header">
                <span class="item-title">American Sign Language Translation (Python)</span>
                <span class="item-date">Aug 2022 – Dec 2022</span>
            </div>
            <div class="item-details">
                <p style="font-style: italic; margin-top: 0;">Collaborated on improving model performance at MIT-IBM Watson AI Lab.</p>
            </div>
        </div>
    </section>
</div>
