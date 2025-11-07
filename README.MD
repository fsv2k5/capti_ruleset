# UML Class Diagram — Filtering Students by Criteria and Developing RuleSet (Backend)


## Purpose
Filter students using an ordered RuleSet based on assessment data. 

Only records with member.role == Student are processed.

## Assessment domain
•	OrganizationMember

•	ReadReadyTestExecution

•	ReadReadySkill (exactly six skills)

•	ReadReadyTestScore

•	ReadReadyMemberInefficientDecoding (depends on the “Word Recognition and Decoding” subtest; if missing -> Unknown).

## Filtering domain
•	RuleSet (ordered)

•	Rule (base with Include/Exclude and order)

•	GradeRule

•	ScaleScoreRule

•	InefficientDecodingRule

•	DecodingThresholdRule


## Key constraints
•	memberId, execution, skill unique in scores;

•	≤1 inefficiency record per (memberId, testExecution);

•	execution/testscore/inefficiency are composition children of their owners;

•	order of rules changes the result.

## Storage idea (PostgreSQL, no DDL)
•	rule_set (meta) + rule (rule_set_id, order_index, rule_type);

•	polymorphism — STI( discriminator) или TPT (subtype tables).
