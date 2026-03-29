---
title: "如何选择AI编程套餐？(Coding Plan)"
tags: ["AI","AI编程","Coding Plan"]
categories: ["AI"]
#externalUrl: ""
#showSummary: true
date: 2026-03-28
draft: false
---

# 如何选择AI编程套餐(Coding Plan)？

主要按计费模式详细介绍一下，尽量用最直观的方式表达。

## 计费模式解析

1. **请求数模式**

这种是云厂商搞的模式。

- 模型请求：**每次思考、每一次连续的输入/输出、每次工具调用、每次命令执行......**，都是模型请求的结果。
- 每次对话可能要进行很多次请求。
- 计费方式比token令人安心，不管你每次请求消耗了多少token，100个token和1亿个token都只计费一次。

**优点**：计费粒度适中，既不会因任务过于复杂而消耗巨量token，也不会因为任务过于简单而一下就消耗了一次Prompt而觉得可惜。

**缺点**：如果你每次处理的都是非常复杂、长时间自动运行的任务，可能消耗比较快。但据我实际使用来看，这种时候很少。

2. **Prompt模式**

这种是国内模型厂商搞的模式，国外的Claude也搞。

- 一次Prompt：输入框输入提示词，一个回车敲过去，直到它正常停止输出。
- 不计算其间消耗的token数和模型调用的次数。

- 一般有5小时滑动窗口：5小时内最多只能发送一定的消息数，还会有周限额。

**优点**：一个长时间自动运行的任务，无论运行多久、输出多少东西，都只消耗一次Prompt。

**缺点**：屁大点事都要消耗一次，比如你跟它说：帮我关机！消耗一次！

3.  **积分单次定额模式**

这种模式现在只有Copilot在搞了。

- “定额”是指不会随输出变长而消耗变多。

- 这里的请求数和上面说的不是一个概念，上面：模型请求；这里：可以当作一种积分。
- 每月定量请求数。
- 每次与AI对话消耗固定的积分/请求数，不计算token。
- 不同模型扣除的额度不同，但不会随输出变长而消耗变多。

**优点**：兼顾高级模型的能力和低级模型的经济，同时还能消除token焦虑。

**缺点**：Copilot的Agent能力还是远不如AI IDE。

这种模式和Prompt模式差不多，但有区别：**Prompt每次给AI发消息只固定消耗1次请求数， 积分单次定额模式会根据模型不同而扣除不同积分/请求数**，例如给Claude Opus 4.6发一条消息可能需要消耗3个请求数，而给GPT-Codex可能只需1个请求数。

4. **积分/美元单次按token计费模式**

这是用的最多的模式，Cursor、Trae、CodeBuddy、Qoder、Claude Code（有两种计费模式）、Kiro、Augment Code都在用。

- 与定额模式的区别：不定额，输入输出越长，消耗积分/美元越多。
- 积分和美元的区别：积分也是用美元兑的，它们与token一级我们口袋里的钱钱都是直接线性相关，换一种代币罢了。

**优点**：没有优点，跟直接消耗token差不多。除非像Kiro这样，每次扣的特别少，但Kiro很容易封号（不过可以薅500积分，能爽几天是几天）。

**缺点**：全是缺点。

5. **积分/请求数日限量模式**

现在使用这种模式的有windsurf（积分称为quota）、Gemini和GPT Codex（每日消息数根据使用的模型和输入输出决定）。

- 每日刷新限额，周额度也有限制。
- 每次对话根据输入输出token计算数计算额度。
- 日额度不得超过上限。
- 使用高级模型->能用的次数少，使用低级模型->能多用几次。

**优点**：不会一下子用完。

**缺点**：你想在某天用它解决顽固bug，可能搞一半就限额了，等明天，甚至等下周，非常恶心，尤其时windsurf。GPT给的额度够到还行，但windsurf是真的狗，它之前是**积分单次定额模式**的，3月19日改了。

## 分类表格

我做了一个表格，这可以看得更直观：（电脑端可收起左侧目录查看）

<div style="width: '100%'; overflow-x: auto;">
    <table>
  <thead>
    <tr>
      <th>计费模式</th>
      <th>原理</th>
      <th>计费模式适用场景</th>
      <th>代表厂商</th>
      <th>价格</th>
      <th>额度</th>
      <th>模型</th>
      <th>备注</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="6">请求数模式</td>
      <td rowspan="6">将每次模型调用作为计数单位，<strong>无需关注每次调用消耗多少token</strong></td>
      <td rowspan="6">零散的<strong>编码</strong>需求、<strong>OpenClaw</strong></td>
      <td><a href="https://www.aliyun.com/benefit/scene/codingplan">阿里云</a>（API+插件）</td>
      <td rowspan="5">Pro：¥200/月；Lite：¥40/月</td>
      <td rowspan="5"><strong>5小时限额</strong>：Lite：1200次，Pro：6000次。<strong>周限额</strong>：Lite：9000次，Pro：45000次。<strong>月限额</strong>：Lite：18000次，Pro：90000次。<strong>大多数很耐用，火山除外</strong></td>
      <td>GLM，Kimi，MiniMax ，Qwen最新开源模型</td>
      <td>稳定，除非上下文特别长才会卡</td>
    </tr>
    <tr>
      <td><a href="https://curl.qcloud.com/BKmhOyJb">腾讯云</a>（API）</td>
      <td>GLM，Kimi，MiniMax，混元最新开源模型</td>
      <td>抢不到，模型少，速度从反馈来看还不错</td>
    </tr>
    <tr>
      <td><a href="https://cloud.baidu.com/product/codingplan.html">百度智能云</a>（API）</td>
      <td>GLM，Kimi，MiniMax，DeepSeek最新开源模型</td>
      <td>模型少，速度从反馈来看还不错，<strong>唯一不敢推自家模型的</strong></td>
    </tr>
    <tr>
      <td><a href="https://volcengine.com/L/CudCK-QJYL4/">火山引擎</a>（API）</td>
      <td>GLM，Kimi，MiniMax，DeepSeek，豆包最新开源模型</td>
      <td>速度慢，超售严重，算力跟不上</td>
    </tr>
    <tr>
      <td><a href="https://www.jdcloud.com/cn/products/jdaip">京东云</a>（API）</td>
      <td>GLM，Kimi，MiniMax最新开源模型，Qwen3-Coder</td>
      <td>前期算力不足，经常请求RPM限制，基本用不了</td>
    </tr>
    <tr>
      <td><a href="https://platform.minimaxi.com/subscribe/token-plan">MiniMax</a>（API）</td>
      <td>¥29/49/119/月三档</td>
      <td>Starter：600次/5小时；Plus：1500次/5小时；Max：4500次/5小时。周限额没明确说。<strong>很耐用</strong></td>
      <td>MiniMax最新模型</td>
      <td>程序员圈内很多人怀疑其跑分造假，不过输出确实快，配合OpenClaw处理普通任务还是不错的</td>
    </tr>
    <tr>
      <td rowspan="2">Prompt模式</td>
      <td rowspan="2">人类发送给AI的一条消息算一个Prompt，<strong>无需关注其间有几次模型请求或多少token消耗</strong></td>
      <td rowspan="2">一个提示词就描述清楚的<strong>复杂任务</strong></td>
      <td><a href="https://www.bigmodel.cn/glm-coding">智谱</a>（API）</td>
      <td>¥49/149/469/月三档</td>
      <td>Lite：约80 Prompt/5小时，400Prompt/周；Pro：约 400 Prompt/5小时，2000 Prompt/周；Max：约1600 Prompt/5小时，8000 Prompt/周。<strong>很耐用</strong></td>
      <td>GLM最新模型</td>
      <td>抢不到，算力仍然不足，模型单一，只有GLM</td>
    </tr>
    <tr>
      <td><a href="https://claude.com/pricing">Claude</a>（API+插件）</td>
      <td>Pro：$20/月；Max 5x：$100/月;Max 20x：¥200/月</td>
      <td>Pro：约45 消息/5小时，300 消息/周；Max 5x：约225消息/5小时，1500消息/周。Max 20x：20倍Pro用量。<strong>比较耐用，但实际跟使用的模型有关</strong>。</td>
      <td>Claude Opus、Sonnet、Haiku最新模型</td>
      <td>公然反华，但确实好用，国内直接开他家基本不可能</td>
    </tr>
    <tr>
      <td>积分单次定额模式</td>
      <td>每次给AI发消息，<strong>根据使用的模型扣除固定额度，不计算token数</strong></td>
      <td>中等复杂度任务</td>
      <td><a href="https://github.com/features/copilot/plans">Copilot</a>（插件）</td>
      <td>Pro：$10/月；Pro+：$39/月</td>
      <td>Pro：300请求数（相当于积分）/月；Pro+：1500请求数。<strong>比较耐用</strong>。</td>
      <td>Claude、Gemini、GPT、Grok最新模型和Raptor（GitHub自研专用模型）</td>
      <td>Copilot的Agent能力不是很好（很不好），不过它有些上古免费模型可以用</td>
    </tr>
    <tr>
      <td rowspan="7">积分/美元单次按token计费模式</td>
      <td rowspan="7">用钱买积分，或直接花钱，消耗积分/钱与token直接相关，<strong>输入输出越多，消耗越多</strong></td>
      <td rowspan="11">小任务</td>
      <td><a href="https://www.trae.ai/pricing">Trae</a>（IDE）</td>
      <td>国际版$10/30/100/月，国内版不推荐（国内模型还按token计费）</td>
      <td>Trae：扣美元，$10可买$20额度，$30可买70额度，$100可买$400额度，按token扣钱，<strong>不耐用</strong>。</td>
      <td>Gemini和GPT的最新模型，不支持Claude，国内版仅支持国内模型，<strong>不推荐付费</strong>。</td>
      <td>直接扣美元额度</td>
    </tr>
    <tr>
      <td><a href="https://qoder.com/pricing">Qoder</a>（IDE）</td>
      <td>$10/30/100/月，不分国内国际</td>
      <td>2000/6000/20000积分/月，<strong>不耐用</strong></td>
      <td>仅支持国内模型，不支持国外的模型，但实际上肯定偷摸用了。</td>
      <td>Agent能力还行，但积分确实不耐用</td>
    </tr>
    <tr>
      <td><a href="https://www.codebuddy.ai/pricing">CodeBuddy</a>（IDE）</td>
      <td>国际个人版仅一个档位$19.9/月</td>
      <td>1000积分，<strong>不耐用</strong></td>
      <td>Gemini和GPT的最新模型，国内版仅支持国内模型，<strong>不推荐付费</strong>。</td>
      <td>不如kiro</td>
    </tr>
    <tr>
      <td><a href="https://cursor.com/pricing">Cursor</a>（IDE）</td>
      <td>$20/60/200/月</td>
      <td>与trae类似，按月付费后获得$20/70/400，然后按原API的token价格计费，直接扣钱，<strong>消耗很快</strong>。自研Composer模型对付费用户<strong>不限额</strong>。</td>
      <td>GPT、Claude、Gemini、Grok、Kimi最新模型。外加"字"研的Composer模型</td>
      <td>贵，直接花token。但是Agent能力超强。</td>
    </tr>
    <tr>
      <td><a href="https://kiro.dev/pricing/">Kiro</a>（IDE）</td>
      <td>$20/40/200/月</td>
      <td>1000/2000/10000积分/月，<strong>比较耐用</strong>。新用户白嫖500积分（免费用户最多能用Sonnet 4.5）。一次普通Opus 4.6任务约花费5积分。</td>
      <td>Claude最新模型，外加DeepSeek、MiniMax、Qwen-Coder-Next</td>
      <td>积分比较耐用，新用户白嫖500积分，但免费用户最多只能用Claude Sonnet 4.5，还很容易封号。</td>
    </tr>
    <tr>
      <td>Augment <a href="https://www.augmentcode.com/pricing">Code</a>（IDE）</td>
      <td>$20/60/200/月</td>
      <td>40000/130000/450000积分每月，一次普通Opus 4.6任务约花费500积分。<strong>不耐用</strong></td>
      <td>Claude最新模型，GPT部分最新模型</td>
      <td>Agent能力也很好，能跟Cursor碰，但积分也是不耐用，跟直接花钱差不多</td>
    </tr>
    <tr>
      <td>Kimi会员（API+Kimi code）</td>
      <td>¥49/99/199/699/月</td>
      <td>5小时+每周限额，百分比显示，无明确额度</td>
      <td>仅支持kimi模型</td>
      <td>网上反馈<strong>比Claude还贵</strong></td>
    </tr>
    <tr>
      <td rowspan="3">积分/请求数限量模式</td>
      <td rowspan="3">每日限总请求数/积分，这个值它可能明说，也可能只显示百分比，根据<strong>使用模型不同、输入输出长短不同，扣除不同额度</strong>。</td>
      <td><a href="https://windsurf.com/pricing">WindSurf</a>（IDE）</td>
      <td>$20/200/月</td>
      <td>每日刷新限额，但没有明确额度，$20的套餐用Opus 4.6，每日只能对话约10次。<strong>用着恼火</strong></td>
      <td>很全面，国外模型：SWE（Codeium自研模型，很一般），GPT、Claude、Gemini、Grok最新模型。国内模型：MiniMax、Kimi、GLM最新开源模型</td>
      <td>不当人了，改了计费方式，丐版15刀涨到20刀，月限额改成日限额和周限额，每天只能和Claude对话七八次。</td>
    </tr>
    <tr>
      <td>Google <a href="https://one.google.com/ai">Gemini</a>（包含Code Assist用于CLI和Antigravity IDE）</td>
      <td>$7.99/19.99（首月0）/249.99（前三月124.99）/月</td>
      <td>200/1000/25000积分/月+Antigravity不定时动态刷新，刷新额度不固定，额度用完花积分。还附带Nano Banana图片、视频生成、Google Drive等权益。最近改完后，<strong>最高档Ultra才够用</strong></td>
      <td>Gemini、Claude、GPT最新模型</td>
      <td>对国内查得严，非常容易封号。额度一降再降。</td>
    </tr>
    <tr>
      <td><a href="https://chatgpt.com/zh-Hans-CN/pricing/">chatGPT</a>（API，包含Codex）</td>
      <td>$8/20/200/月</td>
      <td>$20以上才支持Codex，根据使用模型不同，可使用次数不同，每日刷新，<strong>$20对个人基本够用</strong></td>
      <td>OpenAI最新模型（包含Sora）</td>
      <td>额度多，但付款难，不定时风控。</td>
    </tr>
  </tbody>
</table>
</div>

## 推荐

国内：**阿里云、腾讯云、百度智能云**都可以，京东暂时避坑，火山不行。模型厂商的套餐只有单模型支持，不推荐。

国外：**Kiro、GPT Codex、Copilot**。（如果你能搞定付款的话）三方号容易出问题。

>  联通云、移动云等厂商也有Coding Plan，但我没用过，网上反馈也较少，所以就不推荐了。其实国内还有一家叫UCloud的云计算厂商提供了Coding Plan服务，除了国内模型，还偷摸接了Claude和GPT，但积分及其不耐用，也不推荐了。

下一次我们详解一下如何接入各AI编程工具~