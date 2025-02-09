# AEA: Reviewing and (Pre-) Approving Reports

"Approvers" and "Pre-approvers" will review the reports, and finalize the Summary. 

## Generic Guidance

- Pre-approvals usually can be completed rather quickly and should be prioritized.
- The pre-approver should not be running any of the code or downloading any of the data unless asked to do so.
- The language for the `[REQUIRED]` tag comments is drawn from the [Sample Language for Reports](https://github.com/AEADataEditor/replication-template/blob/master/sample-language-report.md). To ensure uniformity across reports, pre-approvers are encouraged to use the phrases verbatim.

## Preliminary Steps for Pre-approving Reports

1. The "Review for pre-approval" transition in Jira requires specific permissions. If you have not been granted this permission, please reach out to your supervisor. 
2. Clone the Bitbucket repository of the report that requires pre-approval to the local machine or CISER machine. **Do not download the openICPSR deposit!**  The pre-approver checks and finalizes the report but does not redo the whole replication.
  - You can also use "Github Codespaces" for this process.
3. Skim through the report and note if it is an original replication or a revision.  Follow the steps below correspondingly.


## Original Replication Report

1. Verify that the replicator has deleted all of the `INSTRUCTIONS` comments of the report; if not, please do so.
1. Verify if the replication requires **IRB approval/RCT registration**.  These are commonly found in papers that utilize randomized experiments, lab experiments, or surveys run by the authors, involving "human participants."  Ensure that the manuscript contains the necessary approval information (on the title footnote). If absent, insert relevant `[REQUIRED]` or `[SUGGESTED]` tag comments wherever necessary.
1. Read through the **Data Sources section** of the report and check for completeness.
   - Reports sometimes might be missing data sources.  Cross-check (scan) this with the manuscript and the README.  This is usually the most time-intensive part of the pre-approval. 
   - You are not expected to redo this section, but you should spot-check to see if it is complete and accurate.
   - When replicators mention "URL does not work" but provide no further information, verify the URL (if less than 5 URLs to check)
   - The report should accurately reflect whether the data source has been cited and whether its location/access modality has been provided. 
   - Verify/Insert relevant `[REQUIRED]` or `[SUGGESTED]` tag comments.
2. Check the **Data checks section** for completion.
   - Check if the PII scan output is present in the repository.
   - Check if the Package scan output is present in the repository.
   - Verify/Insert relevant `[REQUIRED]` or `[SUGGESTED]` tag comments.
2. Check the **Code checks section** for completion.
   - Check if the completed Code check spreadsheet is present in the repository.
   - Verify/ Insert relevant `[REQUIRED]` or `[SUGGESTED]` tag comments.
4. Check the **Stated Requirements** and **Missing requirements** section for completion and insert relevant `[REQUIRED]` or `[SUGGESTED]` tag comments.
5. Carefully read through the **Replication steps section.**
   - Ensure that this report section is coherent in its description of the steps the replicator took to perform the entire replication. Can you follow the narrative/list of steps, and from it, do you think you understand what the replicator did?
   - If the replicator noted that the code contains bugs, the error message/error code should be explicitly listed.
   - **The pre-approver should not be rerunning any of the code!**
   - Communication between the pre-approver and replicator is encouraged so that any confusing/unclear language used in this section can be clarified.
   - Verify/Insert relevant `[REQUIRED]` or `[SUGGESTED]` tag comments.
6. Check the **Computing Environment of the Replicator section** for completeness. 
7. Verify: Format the results in the **Findings section** into tables by utilizing the the Excel-to-Markdown Extension in Visual Studio.
   - Check if the output/log files have been pushed to the Bitbucket repository.
   - If there are discrepancies between the replicated tables and figures and those of the manuscript, the report should contain images/screenshots to highlight the differences.
   - If there are numerous tables and figures that exhibit discrepancies, these should be put into a .zip file.  This action should be noted in the **Summary section** as well as mentioned in a JIRA comment.
8. Ensure the classification of the replication fits the degree of reproducibility.
9. Fill out the **Action Items** of the report.
   - These are separated into "Manuscript" and "openICPSR" (these sections are pre-existent in the template)
   - Use a script or manually copy-paste all of the `[REQUIRED]` tags to this list.
      - [`aeareq`](https://github.com/AEADataEditor/editor-scripts) extracts the `[REQUIRED]` tags and places them at the top of the REPLICATION.md 
   - Split the action items according to where they can be addressed. Some may be addressable in both sections (for instance, correcting figures and tables, and/or data citations). Others belong only into the "Manuscript" part (IRB, RCT), others only into the "openICPSR" (anything related to code)
   - Order them by importance: `[REQUIRED]` items first, and within these, the most important at the top (correcting bugs, providing missing files).
   - `[SUGGESTED]`  items can be at the end of each section.
      - [`aeareq`](https://github.com/AEADataEditor/editor-scripts) extracts the `[SUGGESTED]`  tags only if provided with the additional argument `sug`
10. Fill out the **Summary section** of the report.
  - Start with a thank you, and a positive note: Highlight the merits of the replication i.e. how many figures/tables were replicated, if data citations were properly completed, etc. 
  - Add a template line with the proposed resolution. These are at the top of the [sample-language-report.md](https://github.com/AEADataEditor/replication-template/blob/master/sample-language-report.md).
11. (Re)generate the PDF of the report.
   - Use MarkdownPDF package if you are using Visual Studio Code
   - Use a script: [`aeaready`](https://github.com/AEADataEditor/editor-scripts) creates the PDF from the REPLICATION.md, crafts the commit message and pushes it to the repository.  It requires additional pieces of software that are noted in the link.
12. Commit and push all changes to the repository.  Advance the JIRA ticket to "Pre-approved."  The pre-approval is now complete!

**Notes:** The pre-approver should reach out to the original replicator for clarifications should there be any confusions during the course of pre-approving the report.  If bugs in the code seem trivial i.e. missing packages, missing `Results` directory, replicator cannot find output etc., the pre-approver should reach out to the original replicator for further clarification.

For the majority of the `[REQUIRED]` comment tags, it is best to use them verbatim to preserve uniformity across our reports.  However, there are times where a more accurate description can help the author pinpoint what exactly is required of them.

For example, say we have a scenario where the author did not include code for Table A.6 in the code deposit but everything else has been provided and replicates perfectly.

Instead of writing:

```
> [REQUIRED] Please provide complete code, including for construction of the analysis data from raw data, and for appendix tables and figures, and identify source for inline numbers.
```

It is clearer to the authors if we write:

```
> [REQUIRED] Please provide complete code for appendix tables and figures, in particular Table A.6.
```


## Revision Report

The checklist of items to review are roughly the same as above.  In addition:

- The pre-approver should check that `[We REQUESTED]` tags are used in place of `[REQUIRED]` tags.  These tags should be preceded by a ">" to create a comment rather than "-," which creates a bullet point.
   - The script [`aeareview`](https://github.com/AEADataEditor/editor-scripts) changes all the `[REQUIRED]` to `[We REQUESTED]`.
- The report should reflect the **current** state of the replication.
- In the **Summary Section:**
   - Create a new section "`### Previously`" that covers all the action items from the previous round.
   - Create a list of persisting issues that require attention. These should be added as action items to the usual section, in addition to any new items. 
   - There is no need to distinguish new from persistent action items: the action item list should simply contain a complete and exhaustive (check)list of items that need to be done.

Example:

```
### Action Items (Manuscript)

- [REQUIRED] The data collection reported in this article had IRB approval. Please provide full IRB approval information, including protocol number and home institution of the IRB, in the titlepage footnote.

### Action Items (openICPSR)

...

### Previously

> [We REQUESTED] The data collection reported in this article had IRB approval. Please provide full IRB approval information, including protocol number and home institution of the IRB, in the titlepage footnote.

Not done. The manuscript still does not mention the IRB information in the titlepage footnote.
```


## Choosing a Recommendation

Approvers must select/confirm one of the recommendations (field `MCRecommendationV2`):

- **Accepted** - the manuscript moves forward in the publishing workflow on Manuscript Central, the Data Editor does not see the manuscript again.
- **Accepted with changes** - same, but some conditions may be imposed. However, the Data Editor does not need to see the manuscript again.
- **Revisions requested - manuscript ready** - Some revisions need to be made, and the Data Editor needs to see the authors' response. However, the manuscript can move forward in the publishing workflow. This is rarely used, but opens up the possibility that the managing editors can pull out a manuscript from this category to move forward, depending on the backlog for publication.
- **Conditional Acceptance** - the Data Editor expects to see a response from the authors to the report.
- **Revise and resubmit** - the Data Editor has detected a serious problem which needs to go back to the "Revise and resubmit" phase of the publishing workflow. This is only invoked if there are significant concerns as to the validity of the manuscript's conclusions based on the reproduction attempt. Rarely used.


## Publication

Once all review rounds have been completed, the last revision will lead to a recommendation of "Accepted". The Data Editor's staff prepares the openICPSR deposit for final publication. In general, this means that a note is added to the "Project Communications Log" on openICPSR, denoting the acceptance of the deposit. The AEA publication staff can subsequently move this issue forward to "Published" when the supplement has been published on openICPSR.

- The field `openICPSRDOI` is pre-filled, but should be checked by the AEA publication staff.

See [Preparing for publication](aea-interfacing-with-the-journal-management-system) for details.
