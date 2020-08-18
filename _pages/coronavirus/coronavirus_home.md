---
permalink: /coronavirus/home
title: "Module 3: Coronavirus"
sidebar:
 nav: "coronavirus"
---

### by Chris Lee and Phillip Compeau

## Introduction: How SARS and COVID-19 Shook the World

### The Onset of SARS

Severe Acute Respiratory Syndrome (SARS or SARS-CoV for coronvirus) made its first appearance in November 2002 Guangdong, China, where the first case of “atypical pneumonia” was reported [^1]. Near the end of the month, the Canadian Global Public Health Intelligence Network and US Global Emerging Infections Surveillance and Response System, partners of the Global Outbreak Alert and Response Network (GOARN), picked up on media reports describing an “influenza outbreak” in Beijing and Guangzhou. The World Health Organization (WHO) requested information from Chinese Authorities and a report was received on 12 December. The details described an investigation of 23 influenza virus isolates, 22 of which confirmed to be type B strains, and how the number of cases were like that of past seasonal patterns. By 11 February 2003, an official report of a severe respiratory syndrome/atypical pneumonia with more than 300 cases and five deaths was received by the WHO by the Chinese Ministry of Health. The WHO Global Influenza Network was alerted by the potential of a presumed new strain of influenza. When Hong Kong authorities reported two cases of A(H5N1) avian influenza on 20 February, WHO influenza pandemic preparedness plans were activated [^2].

On 21 February, a 64 years old Guangdong doctor named Liu Jianlun who had been treating patients with atypical pneumonia, traveled to Hong Kong to attend a wedding while experiencing respiratory symptoms and checked into the Metropole Hotel on the 9th floor. The next day, he was admitted to Kwong Wah Hospital in Kowloon, where he later died on 4 March. Unfortunately, seven guests on the same floor also contracted the disease, including one from the local area, two from Canada, one from Vietnam, and three from Singapore. Upon returning from their trip, the disease was able to spread to Canada, Singapore, Vietnam, and Taiwan, as well as other parts of Hong Kong [^3][^4].

By the middle of March, WHO has received more than 150 new cases in Canada and six Asian countries, and on 15 March, WHO issues an emergency travel advisory global alert along with the disease name SARS. During the containment phase, GOARN recruited laboratory scientists, clinicians, and epidemiologists to provide real-time information, allowing the WHO to provide specific guidance to prevent further spread. Airports began screening individuals for any history of contact with individuals showing SARS-like symptoms to prevent international spread. Eventually, the passengers were asked to avoid traveling to any areas where contact tracing could not link all the cases to known chains of transmission. By 5 July 2003, the SARS outbreak was officially declared to be contained, but not before affecting around 27 countries with 8098 total cases and 774 deaths worldwide [^2][^5]. Later studies identified coronavirus in Chinese horseshoe bats, and in 2017, a population of horseshoe bats in Yunnan province was found to harbor virus strains with all the necessary genetic building blocks to transmit to humans [^6].

### The COVID-19 Pandemic

Severe acute respiratory syndrome coronavirus 2 (SARS-CoV-2) is responsible for the 2019-2020 COVID-19 pandemic that is believed to have started in Wuhan, China. Although not confirmed, it is believed that the first case dates to 17 November 2019 [^7]. On 31 December 2019, the WHO received reports regarding numerous cases of pneumonia of an undetermined cause from the Wuhan Municipal Health Commission. The next day, the WHO activates the three-level Incident Management Support Team to assess the new disease. The disease spread extremely quickly throughout the city where cases doubled every 7.4 days [^8]. By the end of January, 7818 cases were confirmed across 19 countries, resulting in the WHO declaring the sixth Public Health Emergency of International Concern (PHEIC) [^9][^10].

<img src="../_pages/coronavirus/files/WHOReport10.png">

The very next day, Russia, Italy, and United Kingdom reported their first cases of COVID-19 and joined the list affected countries. From then on, the number of COVID-19 cases has exploded, spreading to around 213 countries and territories across the globe as of 17 August 2020.

<img src="../_pages/coronavirus/files/covid19log.png">

<img src="../_pages/coronavirus/files/CovidTable.png">

### Why were they so different?

Just by looking at the name SARS-CoV-2, one can assume that this virus is related to SARS-CoV from 2003. In fact, both viruses belong to the broad coronavirus family, with SARS-CoV-2 being the seventh identified coronavirus to be able to infect humans. So how come the outbreak of SARS and COVID-19 are so different?

Of course, each outbreak is never handled in the exact same way, and differences in both time and approach by authorities will impact the spread of the disease. However, biological differences between the viruses are also key aspects. At the highest level, the most common symptoms between the two are very similar: fever, cough, fatigue, shortness of breath. However, SARS tends to be more severe, with 20-30% of cases requiring mechanical ventilation while an estimated 20% of COVID-19 cases requiring ventilation [^11][^12]. In addition, a key difference in symptoms and transmission is that SARS-CoV-2 can be spread by individuals that are asymptomatic [^13]. In contrast, there are no known cases of SARS from exposure to a SARS patient who has not developed symptoms yet [^14]. This most likely played a major role in international transmission and the attributes to the difficulty in containing the disease.

Investigating the biology of the viruses may also reveal key factors in the outbreak difference. SARS and SARS-CoV-2 viruses belong to the genus Betacoronavirus lineage B. On the whole-genome level, SARS-CoV-2 is most closely related to bat coronaviruses, RaTG13, bat-SL-CoVZC45, and bat-SL-CoVZXC2 with a sequence identity of 96%, 87.99% and 87.23%, respectively, and less genetically similar to SARS-CoV with a sequence identity of about 79% [^15]. However, the method of infection between SARS-CoV-2 and SARS-CoV are strikingly similar. The surface of the viruses is decorated with a transmembrane protein called the Spike protein (S protein). The S protein is critical in the recognition and viral entry into human host cells by binding to the human receptor angiotensin-converting enzyme2 (ACE2) on the host cell surface [^16][^17]. Because of the role the S protein plays, it has become one of the targets in developing a vaccine. 

Even though the S proteins of the two viruses have the same general function, there are still notable differences between the two. Careful analysis of the S protein revealed that the receptor binding domain (RBD), the part of the S protein that directly interacts with ACE2, of SARS-CoV-2 binds to ACE2 with greater affinity [^18]. In addition, the S protein of SARS-CoV-2 was found to be only 75% homologous to the SARS-CoV S protein [^19]. The differences between the two S proteins may reveal why SARS-CoV-2 is much more infectious than SARS.

There are two main objectives for this module. First, we will explore publicly available structure prediction software to model the SARS-CoV-2 S protein and then assess their accuracy. Second, we will visualize and perform comparative analysis on the SARS-CoV-2 S protein and SARS-CoV S protein. All the analysis will be done using two software: ProDy and VMD. By the end of this module, you will be able to understand more about protein structure prediction and differences in the S proteins that attribute to the higher infectivity of COVID-19.


[Protein Structure Prediction](prediction){: .btn .btn--primary .btn--large}
{: style="font-size: 100%; text-align: center;"}


[^1]: CDC SARS Response Timeline. (2013, April 26). Retrieved August 17, 2020, from https://www.cdc.gov/about/history/sars/timeline.htm

[^2]: Heymann, D.L. 2004. The international response to the outbreak of SARS in 2003. Phil. Trans. R. Soc. Lond. B. 359, 1127-1129. DOI 10.1098/rstb.2004.1484

[^3]: Hung L. S. 2003. The SARS epidemic in Hong Kong: what lessons have we learned?. Journal of the Royal Society of Medicine, 96(8), 374–378. https://doi.org/10.1258/jrsm.96.8.374

[^4]: Update 95 - SARS: Chronology of a serial killer. (2015, July 24). Retrieved August 17, 2020, from https://www.who.int/csr/don/2003_07_04/en/

[^5]: SARS. (2017, December 06). https://www.cdc.gov/sars/about/fs-sars.html

[^6]: Cyranoski, D. (2017, December 01). Bat cave solves mystery of deadly SARS virus - and suggests new outbreak could occur. https://www.nature.com/articles/d41586-017-07766-99

[^7]: China's first confirmed Covid-19 case traced back to November 17. (2020, March 13). https://www.scmp.com/news/china/society/article/3074991/coronavirus-chinas-first-confirmed-covid-19-case-traced-back

[^8]: Li, Q., Guan, X., Wu, P., Wang, X., Zhou, L., Tong, Y., Ren, R., Leung, K., Lau, E., Wong, J. Y., Xing, X., Xiang, N., Wu, Y., Li, C., Chen, Q., Li, D., Liu, T., Zhao, J., Liu, M., Tu, W., … Feng, Z. 2020. Early Transmission Dynamics in Wuhan, China, of Novel Coronavirus-Infected Pneumonia. The New England journal of medicine, 382(13), 1199–1207. https://doi.org/10.1056/NEJMoa2001316

[^9]: Statement on the second meeting of the International Health Regulations (2005) Emergency Committee regarding the outbreak of novel coronavirus (2019-nCoV). (2020, January 30). https://www.who.int/news-room/detail/30-01-2020-statement-on-the-second-meeting-of-the-international-health-regulations-(2005)-emergency-committee-regarding-the-outbreak-of-novel-coronavirus-(2019-ncov)

[^10]: Novel Coronavirus(2019-nCoV) Situation Report – 10. (2020, January 30). https://www.who.int/docs/default-source/coronaviruse/situation-reports/20200130-sitrep-10-ncov.pdf?sfvrsn=d0b2e480_2

[^11]: Q&A on coronaviruses (COVID-19). (2020, April 17). https://www.who.int/emergencies/diseases/novel-coronavirus-2019/question-and-answers-hub/q-a-detail/q-a-coronaviruses

[^12]: Paules C.I., Marston H.D., Fauci A.S. 2020. Coronavirus Infections—More Than Just the Common Cold. JAMA. 323(8):707–708. doi:10.1001/jama.2020.0757

[^13]: Tan, J., Liu, S., Zhuang, L., Chen, L., Dong, M., Zhang, J., & Xin, Y. 2020. Transmission and clinical characteristics of asymptomatic patients with SARS-CoV-2 infection. Future Virology, 10.2217/fvl-2020-0087. https://doi.org/10.2217/fvl-2020-0087

[^14]: Severe Acute Respiratory Syndrome (SARS) Frequently Asked Questions. (n.d.) https://www.cdc.gov/sars/about/faq.html

[^15]: Wang, H., Li, X., Li, T., Zhang, S., Wang, L., Wu, X., & Liu, J. 2020. The genetic sequence, origin, and diagnosis of SARS-CoV-2. European journal of clinical microbiology & infectious diseases : official publication of the European Society of Clinical Microbiology, 39(9), 1629–1635. https://doi.org/10.1007/s10096-020-03899-4

[^16]: Shang, J., Ye G., Shi, K., Wan, Y., Luo, C., Aihara, H., Geng, Q., Auerbach, A., Li, F. 2020. Structural basis of receptor recognition by SARS-CoV-2. Nature 581, 221-224.    

[^17]: Li, F., Li, W., Farzan, M., Harrison, S. C. 2005. Structure of SARS Coronavirus Spike Receptor-Binding Domain Complexed with Receptor. Science 309, 1864-1868.  

[^18]: Shang, J., Ye, G., Shi, K. et al. Structural basis of receptor recognition by SARS-CoV-2. Nature 581, 221–224 (2020). https://doi.org/10.1038/s41586-020-2179-y

[^19]: Jaimes, J. A., André, N. M., Chappie, J. S., Millet, J. K., & Whittaker, G. R. 2020. Phylogenetic Analysis and Structural Modeling of SARS-CoV-2 Spike Protein Reveals an Evolutionary Distinct and Proteolytically Sensitive Activation Loop. Journal of molecular biology, 432(10), 3309–3325. https://doi.org/10.1016/j.jmb.2020.04.009



