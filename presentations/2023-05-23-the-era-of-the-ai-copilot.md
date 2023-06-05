# The era of the AI Copilot

## General info

- Date: 23 May 2023
- Event: [[2.records.events.microsoft-build-2023.md]]
- Speaker: Kevin Scott, Microsoft
- URL: https://build.microsoft.com/en-US/sessions/bb8f9d99-0c47-404f-8212-a85fffd3a59d

## Summary

Very good talk introducing the concept of a copilot and a generic architecture stack for building copilots.

A copilot is an AI-based application, typically with a conversational UI, that assists users in cognitive tasks. For example, [ChatGPT](https://openai.com/blog/chatgpt) is an example of a copilot. [GitHub Copilot](https://github.com/features/copilot) is another example.

The copilot stack (developed at Azure) consists of three layers:

1. Frontend
1. Orchestration
1. Model

The frontend layer is basically the user interface of the copilot (similarly as in other types of applications).

The orchestration layer can be divided in two parts:

1. Prompt & response filtering, and metaprompt
1. Grounding and plugin execution

The first part, filters prompts (i.e. user input) as well as responses from the lower layers. The metaprompt part fine-tunes the lower layers by augmenting the prompts and steering them in a certain direction corresponding to what the copilot is supposed to achieve (e.g. requesting the response from the model to be more technical of more casual).

The second part (grounding and plugin execution) consists in gathering additional information to be input to the model along with the prompt. A typical way of grounding is, for example, performing a web search based on the prompt and attaching the resulting information to the prompt before sending it to the model, so that the model has more context to give a better response. This is called Retrieval Augmented Generation (RAG).

This part is also where the execution of plugins happens. A plugin is a component from a third-party that can be plugged into the stack and may do almost anything. In general, plugins often have the following capabilities:

1. Access APIs
1. Retrieve information
1. Perform computations

That means, a plugin may, for example, access an API and perform an action (e.g. making a social media post or making a grocery order), it may search through local documents, or it may execute code. A plugin may run both on the way of the prompt down to the model and/or on the way of the response back to the user (depending on the use case and what the plugin is supposed to achieve). In general, a plugin either augments a prompt (to be sent to the model) or a response (to be sent to the user) with additional information, or has a side effect outside of the copilot.

The lowest layer of the copilot stack (model) is the generative AI model itself, which is deployed on some compute infrastructure.

The proposed architecture stack is supposed to be universal, so that components can be reused in different applications (i.e. different copilots using different models). The plugin system is also supposed to be universal and standardised, so that plugins can run in any copilot. That would mean that independent plugin developers could develop plugins against this interface, and users could then use these plugins for their copilots of choice.

A copilot is not limited to accessing a single model and a single set of plugins. The copilot may access multiple models in sequence and use the response of one model as part of the input for the next model. In this way, specialised models can be used for answering specific parts of the prompt, and the responses of the individual models can be assembled by the copilot to a final answer that is returned to the user.

The talk also presented a very simple [example copilot](https://github.com/microsoft/PodcastCopilot) that demonstrates the chaining of multiple models. The copilot takes an audio file of a podcast as a prompt and then calls multiple models in sequence to generate a social media blurb about the podcast and posts it on LinkedIn. The posting on LinkedIn, for example, is done with a LinkedIn plugin in the copilot stack provided by Azure. The implementation of the entire copilot is only a few hundred lines of Python code.

## Discussion

The copilot stack looks very promising, especially because it's quite simple but seems to allow for very powerful results. The plugin system, with the standardised plugin interface, makes it even more promising. I think that Microsoft is probably a pioneer in this regard, at least I don't know of another company that has a similarly advanced and complete set of platform tools, and a comparable holistic conceptualisation of this area. Microsoft probably wants to lead the field and become the de-facto standard for running AI applications (by also defining some actual technical standards, such as the plugin interface).

I think that at the moment everything is still in the making and not everything has fully converged to a stable state yet (probably many of the services are not generally available yet or are still in preview). However, the pace of development seems to be quite fast and what is being produced seems to be stable and usable (even though it has been developed in a very short time). Of all the three cloud providers, AWS, Microsoft Azure, and GCP, I think that Microsoft pushes the AI capabilities the most.

## Misc

Useful quote:

> The (AI) model is not your product.

It is just infrastructure that enables your product. Thus, don't focus too much on the model, but focus on the architectures, software layers, and platforms that build on top of the model, and that actually constitute your product.
