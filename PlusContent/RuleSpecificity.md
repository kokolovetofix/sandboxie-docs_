# Rule Specificity

Sandboxie prior to build 5.55.0 handled rules exclusivly in a very simple way, a path may be [Closed](ClosedFilePath.md), [Read Only](ReadFilePath.md), [Write Only](WriteFilePath.md), or [Open](OpenFilePath.md) and the priority of rule application was the same, when a closed rule matched a particular path it overruled all other rules.

Staritng with build 1.0.0 Sandboxie-Plus has introduched a new mechanism to evaluate and apply rules, based on how specific thay are and which match level thay have.

The rule specificity is a measure to how well a given rule matches a particular path, simply put the specificity is the length of characters from the begin of the path up to and including the last matching non-wildcard substring. A rule which matches only file types like "*.tmp" would have the highest specificity as it would always match the entire file path.

The process match level has a higher priority than the specificity and describes how a rule applies to a given process. Rules applying by process name or group have the strongest match level, followed by the match by negation (i.e. rules applying to all processes but the given one), while the lowest match levels have global matches, i.e. rules that apply to any process.

For this feature a new type of path directive has been introduced [Normal](NormalFilePath.md) which allows to restore default sandboxing behavioure for a path which parrent have been set to one of the prior 4 types.
