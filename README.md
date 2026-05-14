# Capabilities, Tasks, and Jobs: A Bayesian Hierarchical Meta-Analysis of AI Productivity Effects

> Full implementation plan is available on request.

---

## Abstract

The economics of artificial intelligence is being shaped by three literatures that do not yet speak to one another: the AI capabilities literature that tracks model performance on benchmarks, the experimental productivity literature on what gains AI produces in lab settings, and the labor and macro-economic literature on occupational exposure to AI automation. Each delivers a partial answer to the question of how much of the capability we observe in benchmarks transmits through to tasks, and from tasks through to jobs. This project proposes a **Bayesian hierarchical meta-analysis with partial pooling that integrates the three levels of evidence in one estimation framework**. The primary contribution is fourfold. First, the project quantifies two gaps that the AI economics discussion currently treats qualitatively: the **benchmark-task gap** (model generalization failures, elicitation friction, the human-in-the-loop) and the **task-job gap** (adoption frictions, organizational inertia, equilibrium effects). Second, the framework provides a **comprehensive measurement model for AI capability** that pools dense benchmark data with sparse but economically relevant evidence from academic studies, including a treatment of recent work-adjacent benchmarks (such as OpenAI's GDPval) that lets the data locate them on the spectrum from traditional benchmark to lab study-task. Third, **capability can be translated into real productivity units** (log productivity ratios, and conditionally, wage-bill-equivalent changes), making the structural quantities usable by the labor literature. Fourth, once estimated, the framework supports a range of **decision-relevant functionals**, such as net value calculations for firm-level AI adoption decisions and information value calculations for evaluator-level benchmark portfolio decisions. **Project implementation is organized in phases that derisk progressively**, beginning with the programming domain where evidence is densest, and extending conditionally to broader occupations and to elasticity claims that ultimately connect estimated transmission parameters to the macro debate.


## 1. Motivation

The economics of artificial intelligence (AI) is being shaped by three parallel literatures, largely siloed within their disciplines. The first is the AI capabilities literature, mostly from computer science, which tracks model performance via benchmarks such as HumanEval, SWE-bench, GPQA, and most recently OpenAI's GDPval. The second is the experimental productivity literature which asks how much AI raises measured productivity in specific lab-type settings, including coding with GitHub Copilot (Peng et al., 2023), field deployment of coding assistants (Cui et al., 2026), writing (Noy and Zhang, 2023), customer support (Brynjolfsson, Li, and Raymond, 2025), consulting (Dell'Acqua et al., 2023), and others. The third is the AI exposure literature in the task-based labor framework, beginning with Acemoglu and Restrepo and continuing through Eloundou et al. (2023), which asks whaat tasks different occupations are constituted of and to what degree different occupationsal tasks are exposed to AI. Each delivers a partial answer to the broader question of how much of the capability we observe in model benchmarks transmits through to specific tasks, and from tasks to real-world jobs.

This project proposes a Bayesian hierarchical meta-analysis that integrates the three levels of evidence in a single estimation framework: benchmark observations at the model-task level, lab study effect sizes at the task level, and productivity changes in the field at the job level. The hierarchical structure addresses sparse evidence within each level (e.g., few studies per task type in lab studies) by partially pooling subgroup-level parameter estimates towards population-level means, with the strength of pooling determined by the data rather than the analyst. The framing of the framework is borrowed from the AI exposure literature in economics where the task-based approach to labor dominates. The project's role is to put empirical content on the arrows that represent the rates at which capability transmits through to job performance. Treating latent capability as the common construct linking the three levels, this framework also provides a more integrated way to measure and track AI capabilities.

## 2. Contribution

This project makes four primary contributions:

First and most substantively, the project quantifies two gaps that the AI economics discussion currently treats qualitatively. The **benchmark-task gap** captures the loss of capability between what models can do in isolation and what humans using those models can do in lab studies. This gap is presumed to exist because of model generalization failures, elicitation friction, and the human-in-the-loop, but it has not been quantified in a unified framework. The **task-job gap** captures the further loss between lab task performance and field productivity. This gap is presumed to reflect adoption frictions, organizational inertia, and equilibrium effects, but has likewise not been quantified. The project provides a framework to discipline these debates, and produces structural estimates of the cross-task means $\mu^{\text{lab}}$ and $\mu^{\text{field}}$ as headline transmission parameters at each gap. The directional expectation, registered ex ante, is that $\mu^{\text{field}} < \mu^{\text{lab}}$: adoption frictions exceed model-generalization frictions.

Second, the framework provides a **measurement model for AI capability** that pools dense benchmark data with sparse but economically relevant study evidence, a tool the AI exposure literature currently lacks. It also locates recent work-adjacent benchmarks (such as OpenAI's GDPval) and human-curated benchmarks that capture complex real-world tasks (such as codearena) on the spectrum from traditional benchmark to lab study-task, letting the data speak to where they actually sit.

Third, the framework translates **model capability to real productivity units** (i.e., log productivity ratios, and conditionally, wage-bill-equivalent changes). This allows its structural quantities to directly inform the debate around real productivity effects of AI in labor and macro economics.

Fourth, with the joint posterior over capability and transmission parameters in hand, the framework allows estimating a range of **decision-relevant functionals** that map onto different stakeholder questions. Two appear to be of particular value: i) information value calculation for benchmark portfolio decisions that quantifies how much each benchmark reduces uncertainty in downstream transmission and productivity quantities, and ii) net value calculation for firm-level adoption decisions that compares productivity gains with token costs and wages to determine at what capability level AI becomes economically rational for which tasks at which wage levels. These applications show the versatility of this framework: they are differemt lenses read off the same posterior.

This is first and foremost a measurement and structural meta-analysis project. It estimates how AI capability transmits from benchmark to task to job, and translates the result into productivity statements in real units. It provides the structural quantities that macro-forecasts and claims of aggregate AI impact rest on. It is not a critique of any individual study or benchmark. Instead, it pools the existing evidence using the structure of the AI exposure literature, and reports what that pooled evidence implies. The project is complementary to recent efforts in CS to benchmark on more realistic task sets (e.g., ProgramBench, Continual Learning Bench) and with the literature on open-world evaluations (e.g., Kapoor et al. 2026), which qualitatively characterizes upper-bound capability through long-horizon real-world tasks. This project provides the quantitative complement, estimating average transmission across the space of evidence that supports partial pooling.


## 3. Implementation risk and framing

The biggest risk to this project at its initial stage is the coverage at the tuple-level of $(\text{study-task}, \text{time}, \text{task type})$. With an expected 30-80 *study-task observations* across three task families, several years, and multiple model versions, identification of task-specific transmission parameters will be largely shrinkage-driven. The framing the data can support is therefore identification of the cross-task means $\mu^{\text{lab}}$ and $\mu^{\text{field}}$ as headline structural quantities, with task-specific deviations as secondary outputs whose credible intervals will reflect the data scarcity honestly. Whether even the cross-task means are estimated precisely enough to support point-estimation framing, or only bounds, is itself an empirical question, addressed by a power analysis prerequisite to any final fit.

For extensions into occupational categories beyond coding tasks, access to GDPval facet-level data would be helpful but is not a necessary condition for the project to be useful. The model can be run at occupation-level granularity and still provide interesting insights for the programming domain specifically. The deeper goal of connecting evidence from the lab and field to aggregate elasticity claims is conditional on the availability of field-study labor-input data, and is treated as an extension rather than a core part of the project. One productive way of looking at these uncertainties is not through the lens of immediate feasibility but in terms of a timeline: as evaluative work on the capabilities and economic impacts of AI is rapidly accumulating, analyses that are unsupported today will likely become feasible in the near future. The phased implementation strategy ensures that, at each stage, there is a defined deliverable that does not depend on any future stage succeeding.


## 4. Setup and notation

The unit of analysis at the bottom of the hierarchy is the **study-task**: a single treatment effect reported in a single study on a relevant task. A study reporting effects on three tasks contributes three study-tasks. Each study-task is associated with a **task type** $k$, suggsted to be drawn from a rather coarse three-pronged taxonomy designed for the headline aggregation: short-form code generation (HumanEval, MBPP-style items), repo-level debugging (SWE-bench, LiveCodeBench), and agentic or long-horizon work (METR's HCAST, RE-Bench). A finer taxonomy is likely unwarranted given the data. Running the model at different aggregation levels is suggested as robustness check. For the mapping of benchmark items and study-tasks each to one of the three categories, the plan is to use large language models and publish the resulting associations alongside the paper.

Each study-task is associated with a **model** $m$ and a **time** $t$ (likely the calendar quarter at which the study was run, or at which the model was released, depending on data availability). The structural estimation in the lab and field layers will likely be restricted to closed frontier models as the academic productivity literature is essentially exclusively on closed models (Copilot, GPT-3.5/4/4o, Claude). The transmission parameters thus carry the explicit interpretation of "passthrough rates for frontier closed models." Note, the benchmark layer can still include open-weight models for plausibility checks, but they sit outside the structural model.

Each occupation $j$ is associated with **task bundle weights** $w_{k,j}$, taken from the O\*NET dataset (the U.S. Department of Labor's Occupational Information Network), that sum to one over task types $k$ for each occupation $j$. The weights represent the share of an occupation's total work activity accounted for by task type $k$. The AI exposure literature, beginning with Felten, Raj, and Seamans (2018) and Webb (2020) and continuing through Eloundou et al. (2023), uses these weights to aggregate task-level exposure scores into occupation-level exposure indices. This project adopts the same aggregation rule but for capability estimates instead of exposure scores.


## 5. Framework overview

The framework integrates three levels of evidence onto a common scale of latent capability $\theta_{m,k,t}$, which is a unitless logit-scale measure of model $m$'s capability on task type $k$ at time $t$.

**Benchmark layer.** Latent capability is recovered from per-item benchmark performance using two-parameter logistic Item Response Theory (IRT). Borrowed from the psychonometric literature, the IRT parameters separate model capability from item difficulty. This pools evidence across heterogeneous benchmarks (HumanEval, SWE-bench Verified, LiveCodeBench, and agentic benchmarks like METR HCAST and RE-Bench) onto a common scale. This framework also allows recent work-adjacent benchmarks (GDPval, ProgramBench) to enter as an intermediate measurement level. Rather than imposing their exact position relative to traditional benchmarks and lab study-tasks by editorial choice, we let the data identify where these more realistic benchmarks sit on the ecological-validity spectrum. This is arguably itself an interesting empirical output of the framework.

**Lab layer.** Lab studies report standardized treatment effects of AI assistance on more narrowly circumscribed tasks. The link from latent capability $\theta$ to observed effect size $\hat\tau_s$ is specified as a saturating function (rather than linear) to capture the empirical pattern of diminishing returns of productivity gains to model capability:

$$
\hat\tau_s = \alpha_{k(s)} + \lambda^{\text{lab}}_{k(s)} \cdot f\bigl(\tilde\theta_{m(s),k(s),t(s)}\bigr) + X_s'\beta + u_s
$$

where:
- $\lambda^{\text{lab}}_k$ is the rate at which raw capability passes through to register as a measured effect
- $f(\cdot)$ is a saturating link function
- $\tilde\theta$ is the orthogonalized capability (against calendar time, to disentangle capability gains from concurrent improvements in tooling, scaffolding, prompting, etc.)
- $X_s$ is a set of study-level covariates (design, participant population, scaffolding support).

Task-specific transmission rates $\lambda^{\text{lab}}_k$ are partially pooled via the hyperprior $\lambda^{\text{lab}}_k \sim \mathcal{N}(\mu^{\text{lab}}, (\tau^{\text{lab}})^2)$, with $\mu^{\text{lab}}$ the cross-task mean transmission rate and $\tau^{\text{lab}}$ its cross-task standard deviation. Given the expected data scarcity at the task level, the headline parameter may end up being $\mu^{\text{lab}}$, rather than individual $\lambda^{\text{lab}}_k$.

Identification of $\lambda^{\text{lab}}_k$​ requires care because two distinct quantities both link capability to observed effect size: (i) the transmission $\lambda^{\text{lab}}_k$ (capability to log-productivity, which is the object of interest) and (ii) the measurement-scale conversion $\gamma_k$ (log-productivity to Cohen's $d$, which is a nuisance parameter that varies with experimental design, cohort heterogeneity, among others). Studies that report only standardized effect sizes identify the product $\lambda^{\text{lab}}_k \cdot \gamma_k$, but not the two pieces separately. The model addresses this by splitting the problem into two parts that the data can identify separately. The first piece, $\psi_k$, measures how strongly observed effect sizes $d$ rise with capability $\theta$ across all lab studies. This is identified from the full sample. The second piece, $\gamma_k$, measures how strongly log-productivity gains rise with capability. This is identified from the subset of studies that report time-on-task or throughput in physical units. The transmission parameter $\lambda^{\text{lab}}_k = \psi_k \cdot \gamma_k$ then drops out as a derived quantity rather than being estimated directly as each piece is pinned down by a different part of the data.

**Field layer.** Field studies report productivity changes for occupations under AI deployment. Capability enters via the task-bundle aggregation, with $\lambda^{\text{field}}_j$ measuring the impact of task-level capability on job-level productivity given firm adoption, worker-tool matching, and labor-market response:

$$
\hat\Delta_{s'} = \beta_{j(s')} + \lambda^{\text{field}}_{j(s')} \cdot \sum_k w_{k,j(s')} \cdot \tilde\theta_{m(s'),k,t(s')} + X_{s'}'\beta + v_{s'}
$$

where:
- $\lambda^{\text{field}}_{j(s')}$ is the rate at which raw capability passes through to register as a productivity-enhancing effect

The composite $\mu^{\text{lab}} \cdot \mu^{\text{field}}$ is the headline benchmark-to-job passthrough, with $\mu^{\text{lab}}$ and $\mu^{\text{field}}$ being the hyper-means of the distributions which $\lambda^{\text{lab}}_k$ and \lambda^{\text{field}}_{j(s')} are drawn from.

As above with $\lambda^{\text{lab}}_k$, $\lambda^{\text{field}}_{j(s')}$ are partially pooled via the hyperprior $\lambda^{\text{field}}_{j(s')} \sim \mathcal{N}(\mu^{\text{field}}, (\tau^{\text{field}})^2)$, with $\mu^{\text{field}}$ the cross-task mean transmission rate and $\tau^{\text{field}}$ its cross-task standard deviation.

**Productivity calibration.** A subset of lab studies report time-on-task or throughput in physical units. These will be used to translate latent capability into log productivity ratios via task-type-specific calibration $\gamma_k$, so every $\theta$ posterior has a real-units interpretation. A worker on task type $k$ using a model with capability $\theta$ produces $\exp(\gamma_k \cdot \tilde\theta)$ times as much per unit time as an unassisted worker.

**Smoothness over time.** Capability evolution over time is modeled with a Gaussian process prior with Matérn-3/2 kernel for each (model family, task type) pair. The kernel choice produces moderately-smooth trajectories that importantly do allow for occasional sharper changes around major model releases, but rule out implausibly jagged ones. A capability-index alternative (a benchmark-composite frontier index) will be reported as robustness.

**Estimator.** The model is fit in a modular Bayesian workflow in two stages. Stage 1 fits IRT separately per benchmark family, recovering posterior draws of latent capability with measurement-error variance. Stage 2 is the meta-regression with $\lambda$, $\gamma$, the Gaussian process on capability over time, and the study-level covariate adjustments, treating Stage 1 posteriors as measurement-error inputs via multiple imputation. The benefits are computational tractability for joint posteriors that would otherwise not mix, principled handling of benchmarks with only aggregate (that is, non-item-level) data, and graceful degradation in cells with low coverage. The cost, on the other hand, is some efficiency loss.

**Bayesian approach.** A Bayesian hierarchical approach is the right tool here for three reasons. First, partial pooling across multiple levels (i.e., multiple items within benchmarks, multiple task types within domains, multiple studies within task types, and multiple time points within model families) is what supplies stable estimates given the small intersection of evidence types. Second, latent capability is a measurement-model construct identified jointly across the three levels. A Frequentist two-step approach easily understates uncertainty and induces attenuation bias. And third, downstream economic quantities of interest are functionals of the posterior, and hence natural to obtain (whereas harder to model naturally in a Frequentist framework).

## 6. Identification, threats, and falsification

The headline parameters are the cross-task means $\mu^{\text{lab}}$ and $\mu^{\text{field}}$. Task-specific deviations are reported as secondary and are largely shrinkage-driven where data are sparse.

**Power.** Whether the headline means $\mu^{\text{lab}}$ and $\mu^{\text{field}}$ support direct estimation or require bounding is itself an empirical question. We address this through power analysis: the simulation generates data under the full specification, fits the model under realistic data scarcity, and reports expected credible-interval widths. This determines the framing of the headline results before any final fit.

**Threats to identification.** Six threats warrant an explicit, ex ante response:

1. *Potential selection of task type into study type* is acknowledged but not solved. The plan is to report transmission parameters for the union and intersection of selected task types separately, and to discuss the gap.
2. *Classic publication bias* is addressed via a classic monotonic selection model with sensitivity parameter, with results reported under multiple values to characterize sensitivity of the results to different realistic magnitudes of the file-drawer effect.
3. Another possibility is *survivorship bias* of novel attention-grabbing results in this young literature, and that effect sizes may systematically decline as the literature matures. This could potentially be addressed via an Andrews-Kasy specification-curve diagnostic, conditional on study publication date.
4. *Benchmark contamination* is handled by fitting the model twice, once on the full benchmark set and once on a subset assumed to be (more) contamination-resistant (i.e., LiveCodeBench with date-rotated problems, SWE-bench Verified, METR HCAST, RE-Bench). The plan is to discuss the stability of transmission estimates across these two fits.
5. *Stationarity of O\*NET task-bundle weights.* Treating $w_{k,j}$ as fixed data ignores worker reallocation across tasks under AI deployment, which biases inferred field transmission downward. The plan is to address this with a bounding exercise: a lower bound under full reallocation using exposure-derived adjustments, an upper bound under fixed pre-AI weights. If the bound width exceeds posterior uncertainty on $\mu^{\text{field}}$, one read would be that the weight assumption dominates statistical uncertainty. This should be transparently reported.
6. *Tooling, prompting, and scaffolding* remain confounders even after study-level covariate adjustments. Rather than claiming to solve this, the transmission parameters are interpreted as associational structural parameters, not causal ones. The structural content is the partial-pooling architecture and the cross-tier linkage, not a causal claim on $\theta \to$ productivity holding deployment context fixed.

**Falsification.** It is important to think about what, for each layer of the model, would constitute a failure mode:

1. The *IRT measurement* would straight-forwardly be falsified if capability trajectories over time were non-monotonic within a model family on contamination-resistant benchmarks, as this would go against the general notion of consistent technical progress. Another failiure mode concerns the notion that benchmarks may not be measuring a common latent. One diagnostic test would operate on the linking model itself: if the benchmark-specific biases $\delta_b$ in $\theta^b_{m,t} = \theta_{m,k,t} + \delta_b + \eta_{b,m,t}$ are large relative to the cross-model variation in $\theta_{m,k,t}$, the benchmarks are probably measuring different latents and Stage 2 pooling is misspecified.
2. The *structural identification of transmission gaps* would likely be falsified, or its ability to yield insightful results at least be called into serious question, if credible intervals on the transmission means included zero.
3. *Productivity statements* should probably not be generalized from the time-reporting subsample to the full sample if productivity calibration spanned more than an order of magnitude in implied gains for typical capability values.


## 7. Decision-relevant functionals

With the joint posterior over capability and transmission parameters estimated, the framework supports a range of functionals that address different stakeholder questions. Two are developed in detail because they are arguably of particular importance in the current AI economics discussion, which treats them only qualitatively.

**Net value per task.** The first functional combines productivity gains with token costs and occupational wages to produce net value per task, model, and time:

$$
\text{NetValue}_{m,k,t} = w_k \cdot \bigl(\exp(\gamma_k \cdot \tilde\theta_{m,k,t}) - 1\bigr) \cdot T_k - p_m \cdot Q_{m,k}
$$

where:
- $w_k$ is the hourly wage
- $T_k$ is task duration in the absence of AI
- $p_m$ is the per-token price
- $Q_{m,k}$ is tokens consumed per task (modeled as log-normal rather than fixed, reflecting the fact that reasoning models on hard tasks vary by an order of magnitude across prompts)

The substantive question is at what capability level AI becomes economically rational for a particular tasks given wage levels. The output is directly useful for firm decisions, the AI-adoption literature (e.g., Bick, Blandin, and Deming, 2024), and policy modeling. A variance decomposition can be used to disentangle how much of the uncertainty in net value can be attributed to productivity mapping, wages, prices, or token consumption. If productivity mapping dominates, that would arguably itself be a policy-relevant finding.

**Information value-added of benchmarks.** The second functional asks how much each benchmark contributes to reducing uncertainty in transmission and productivity quantities. The natural object of interest is the variance reduction in a parameter (such as $\mu^{\text{lab}}$ or implied productivity at a given capability) conditional on inclusion of a particular benchmark in the data. Normalized by the cost of producing or maintaining the benchmark, this yields an information value per dollar akin to formal cost-benefit analysis that supports benchmark portfolio decisions. Its application includes questions such as which benchmarks to build next, which to maintain, which to retire. The same logic extends prospectively to proposed benchmarks via prior predictive simulation under hypothesized characteristics. This output provides the appropriate marginal-value framing to a discussion the AI evaluation community often only grapples with in absolute terms (i.e. "granted their weaknesses, it is better to have benchmarks than to have none").

The above are illustrations rather than an exhaustive list of potential outputs. The framework is a general-purpose engine, and the two functionals described are arguably the ones with the highest immediate value to stakeholders in AI economics and AI evaluation. Other sufficiently well-defined functional, however, can be thought of and derived with appropriate uncertainty propagation.


## 8. Phased implementation

The project proceeds in phases that derisk progressively. The core is accomplished in Phase 1, and is arguably a viable contribution to the debate in and of itself. Later phases extend this contribution substantially but are conditional on data access and time.

**Phase 1: Programming domain.** This phase is entirely focused on the most data-rich subset of teh data: programming benchmarks, programming lab studies, and programming field studies, with productivity calibration via the time-reporting subsample. Joint estimation of latent capability, lab and field transmission parameters, and productivity calibration on the programming domain primarily, with related occupations as data permit. Phase 1 produces cross-task transmission means, capability-time trajectory for major model families, real-unit productivity calibration, the posterior on the ecological-validity location of integrated benchmarks (such as GDPval), and the two decision-relevant functionals. Programming is the right starting point because data density is highest at all three levels and task definitions are likely cleanest. The contribution of Phase 1 arguably stands on its own.

**Phase 2: Extension to GDPval-covered occupations.** This phase extends the framework to non-programming task types and occupations. Planned outputs are cross-occupation transmission parameters that test whether the programming gap generalizes. Thsi phase requires facet-level access to GDPval data. Without it, the model degrades to occupation-level granularity, weakening the bundle decomposition for non-programming occupations but preserving the overall framework.

**Further extensions:** 
1. One natural extension to work on is to clearly connect outputs of teh present framework to the to the macro-AI debate around Acemoglu's modest and Brynjolfsson's larger aggregate estimates.
A wage-bill-equivalent translation would combine field productivity changes with observed labor inputs and occupational wage data, enabling a structural connection from estimated transmission parameters to labor demand elasticities. This is conditional on field studies reporting labor inputs at sufficient granularity.
2. A further extension generalizes the additive lab specification to a CES production function, identified for the subset of task types with skill-stratified evidence. This would address the active disagreement between studies finding skill-leveling effects (Brynjolfsson, Li, Raymond, 2025) and those finding skill-amplifying effects (Dell'Acqua et al., 2023).
3. Another refinement would investigate the finer underlying ecological-validity structure to our coarse discrete instrument levels from Phase 1. Letting instruments vary smoothly by ecological validity, maybe with a parametric specification on a small number of ex-ante dimensions of this validity dimension (human-in-the-loop, task horizon, grading mechanism), would allow for a much more granular debate on the extent to which benchmarks and adjacent instrument likely transate into job-relevant productivity effects.


## References

Acemoglu, D., and Restrepo, P. (2018). The race between man and machine: Implications of technology for growth, factor shares, and employment. *American Economic Review*, 108(6).

Acemoglu, D., and Restrepo, P. (2020). Robots and jobs: Evidence from US labor markets. *Journal of Political Economy*, 128(6).

Acemoglu, D. (2024). The simple macroeconomics of AI. *Economic Policy*, 40(121), 13–58.

Bick, A., Blandin, A., and Deming, D. (2024). The rapid adoption of generative AI. *NBER working paper*.

Brynjolfsson, E., Li, D., and Raymond, L. (2025). Generative AI at work. *Quarterly Journal of Economics*, 140(2).

Crosta, T., Karlan, D., Ong, F., Rüschenpöhler, J., and Udry, C.R. (2025). Unconditional Cash Transfers: A Bayesian Meta-Analysis of Randomized Evaluations in Low and Middle Income Countries. *NBER working paper*.

Cui, Z., Demirer, M., Jaffe, S., Musolff, L., Peng, S., and Salz, T. (2026). The effects of Generative AI on high-skilled work: Evidence from three field experiments with software developers. *Management Science*.

Dell'Acqua, F., et al. (2023). Navigating the Jagged Technological Frontier: Field Experimental Evidence of the Effects of Artificial Intelligence on Knowledge Worker Productivity and Quality. *Management Science*, 37(2), 403-422.

Eloundou, T., Manning, S., Mishkin, P., and Rock, D. (2024). GPTs are GPTs: Labor market impact potential of large language models. *Science*, 384(6702).

Felten, E. W., Raj, M., and Seamans, R. (2018). A method to link advances in artificial intelligence to occupational abilities. *AEA Papers and Proceedings*, 108.

Kapoor, S., Kirgis, P., Schwartz, A., Rabanser, S., et al. (2026). Open-world evaluations for measuring frontier AI capabilities. *Working paper*.

METR (2025). HCAST: Human-Calibrated Autonomy Software Tasks. *Working paper*.

Noy, S., and Zhang, W. (2023). Experimental evidence on the productivity effects of generative artificial intelligence. *Science*, 381(6654).

OpenAI (2025). GDPval: Evaluating AI on economically valuable tasks.

Peng, S., Kalliamvakou, E., Cihon, P., and Demirer, M. (2023). The impact of AI on developer productivity: Evidence from GitHub Copilot. *Working paper*.

The Continual Learning Bench Team (2026). Continual Learning 1.0. Available at: https://continual-learning-bench.com/news/cl-bench-1-0/.

Webb, M. (2020). The impact of artificial intelligence on the labor market. *Working paper*.

Yang et al. (2025). Evaluating and Aligning CodeLLMs on Human Preference. Available et: https://codearenaeval.github.io/.

Yang et al. (2026). ProgramBench: Can Language Models Rebuild Programs From Scratch? *Working paper*.
