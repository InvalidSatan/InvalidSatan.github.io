<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Generative AI Tools Presentation</title>

  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com" defer></script>

  <!-- React 18 (UMD builds) -->
  <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin defer></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin defer></script>

  <!-- Lucide‑React (correct UMD build) -->
  <script src="https://unpkg.com/lucide-react@latest/umd/lucide-react.development.js" crossorigin defer></script>

  <!-- Babel — inline JSX transformer (keep last so it can transform inline scripts) -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>
<body class="bg-gray-900">
  <!-- React root -->
  <div id="root"></div>

  <!-- Presentation code compiled by Babel in‑browser -->
  <script type="text/babel">
    /**
     * Waits until React, ReactDOM, and LucideReact are on the window before bootstrapping.
     * This avoids race‑condition errors on slow connections.
     */
    function runWhenLibsAreReady() {
      const libCheck = setInterval(() => {
        if (
          window.React &&
          window.ReactDOM &&
          (window.LucideReact || window.lucideReact)
        ) {
          clearInterval(libCheck);

          // Some CDN builds expose `lucideReact` instead of `LucideReact` – normalise it.
          if (!window.LucideReact) {
            window.LucideReact = window.lucideReact;
          }

          initializeApp();
        }
      }, 100);
    }

    /**
     * Main application – all presentation logic lives here.
     */
    function initializeApp() {
      // Destructure only the icons we actually use.
      const {
        ChevronLeft,
        ChevronRight,
        GraduationCap,
        Zap,
        Building,
        Bot,
        BrainCircuit,
        BotMessageSquare,
        FileText,
        Lightbulb,
      } = window.LucideReact;

      // -----------------------------
      //  Presentation Data
      // -----------------------------
      const presentationData = [
        {
          type: "title",
          title: "Generative AI Tool Tiers and Features for Higher Education",
          subtitle: "A Comparative Overview for Institutional Decision-Making",
        },
        {
          type: "intro",
          title: "Common AI Tool Tier Structure",
          points: [
            {
              title: "Free / Basic Tiers",
              content:
                "Access to baseline models (e.g., GPT‑3.5) with limited usage quotas and features. Good for casual use but often restrictive for in‑depth academic work.",
              icon: "GraduationCap",
            },
            {
              title: "Pro / Premium Tiers (~$20/month)",
              content:
                "Unlock advanced models (e.g., GPT‑4 class), offering higher usage limits, priority access, and powerful features like code interpreters, advanced web research, and multimodal capabilities.",
              icon: "Zap",
            },
            {
              title: "Enterprise / Education Tiers",
              content:
                "Designed for organizations. Provide very high or unlimited usage, enhanced security, data privacy, admin controls, and collaboration tools, often with educational discounts.",
              icon: "Building",
            },
          ],
        },
        {
          type: "tool",
          toolName: "OpenAI ChatGPT",
          icon: "Bot",
          tiers: [
            {
              name: "Free",
              price: "$0",
              features: [
                "GPT‑3.5 & limited GPT‑4o access",
                "~10 messages every 3 hours",
                "Web browsing & basic image generation",
                "Slower response times during peak hours",
              ],
            },
            {
              name: "Plus",
              price: "$20/mo",
              features: [
                "Full access to GPT‑4 models",
                "~80 messages every 3 hours (8× free)",
                "Advanced Data Analysis (Code Interpreter)",
                "Plugins, DALL‑E image generation, advanced voice/vision",
              ],
            },
            {
              name: "Pro",
              price: "$200/mo",
              features: [
                "\"Near‑unlimited\" usage caps",
                "Access to highest‑performance models",
                "Early access to experimental features",
                "For heavy professional/research use",
              ],
            },
            {
              name: "Edu / Enterprise",
              price: "Custom",
              features: [
                "Campus‑wide GPT‑4 access",
                "Enhanced data privacy & security (SSO)",
                "Admin controls & shared workspaces",
                "Longer context windows for large documents",
              ],
            },
          ],
        },
        {
          type: "tool",
          toolName: "Google Gemini",
          icon: "BrainCircuit",
          tiers: [
            {
              name: "Free",
              price: "$0",
              features: [
                "Standard Gemini model in Google apps",
                "Basic \"Help Me Write\" features",
                "Limited deep research & context",
                "Imagen 4 for basic image generation",
              ],
            },
            {
              name: "AI Pro",
              price: "$20/mo",
              features: [
                "Powerful Gemini 2.5 Pro model",
                "Full \"Deep Research\" web analysis",
                "Gemini in Chrome for page summaries",
                "Includes NotebookLM Plus & 2 TB storage",
                "<strong class='text-yellow-300'>Free for college students until end of 2026</strong>",
              ],
            },
            {
              name: "AI Ultra",
              price: "$250/mo",
              features: [
                "Most advanced model: Gemini 2.5 Pro \"Deep Think\"",
                "Massive 1 million‑token context window",
                "Advanced video generation (Veo 3)",
                "Agentic AI (Project Mariner) previews",
              ],
            },
          ],
        },
        {
          type: "tool",
          toolName: "Anthropic Claude",
          icon: "BotMessageSquare",
          tiers: [
            {
              name: "Free",
              price: "$0",
              features: [
                "Excellent for long text analysis",
                "Large 100 k token context window (~75 k words)",
                "Strict message cap: ~9 messages every 5 hours",
                "Good conversational tone",
              ],
            },
            {
              name: "Pro",
              price: "$20/mo",
              features: [
                "At least 5× more usage (~45+ messages/5 hrs)",
                "Access to strongest models (Claude 3 Opus)",
                "Claude Code (CLI assistant)",
                "Google Workspace integration",
              ],
            },
            {
              name: "Max",
              price: "$100+/mo",
              features: [
                "5×–20× the Pro usage limit",
                "Priority access during high‑traffic periods",
                "Effectively removes practical limits for heavy use",
                "Early access to new features",
              ],
            },
            {
              name: "Edu / Enterprise",
              price: "Custom",
              features: [
                "Access to 200 k token context models",
                "Campus‑wide access with discounts",
                "Centralized administration and security",
                "Specialized academic research mode",
              ],
            },
          ],
        },
        {
          type: "tool",
          toolName: "Google NotebookLM",
          icon: "FileText",
          tiers: [
            {
              name: "Free",
              price: "$0",
              features: [
                "AI research assistant for your documents",
                "Create up to 100 notebooks",
                "Up to 50 sources per notebook",
                "Limited daily queries & audio overviews",
              ],
            },
            {
              name: "Plus",
              price: "Included with Gemini Pro",
              features: [
                "5× higher limits (500 notebooks, 300 sources)",
                "5× more queries & audio overviews",
                "Customize AI tone (e.g., tutor vs. assistant)",
                "Collaboration: Share notebooks with peers",
              ],
            },
          ],
          note:
            "NotebookLM is specialised for source‑grounded Q&A, not a general‑purpose chatbot. It excels at helping students and researchers analyse and synthesise their own course materials and readings.",
        },
        {
          type: "comparison",
          title: "At‑a‑Glance Comparison (Pro Tiers)",
          headers: ["Feature", "ChatGPT Plus", "Gemini AI Pro", "Claude Pro"],
          rows: [
            ["Monthly Cost", "$20", "$20", "$20"],
            ["Core Strength", "Versatility & Tools", "Ecosystem Integration", "Long Document Analysis"],
            [
              "Key Features",
              "Code Interpreter, Plugins, DALL‑E 3",
              "Deep Research, Chrome/Workspace AI, Video Gen",
              "100 k+ Token Context, Claude Code (CLI)",
            ],
            ["Usage Limits", "~80 GPT‑4 msgs / 3 hrs", "Generous limits, 1 k monthly video credits", "~45+ msgs / 5 hrs"],
            [
              "Unique Perk",
              "Largest ecosystem of custom GPTs",
              "Bundled w/ NotebookLM Plus & 2 TB Drive",
              "Superior performance on summarising books/long PDFs",
            ],
            [
              "Best For…",
              "Students/faculty needing a powerful, all‑in‑one creative and analytical tool.",
              "Users heavily invested in the Google ecosystem (Docs, Gmail, Drive).",
              "Humanities, law, and research fields involving extensive reading.",
            ],
          ],
        },
        {
          type: "conclusion",
          title: "Conclusion: The Value of Premium Access",
          points: [
            "Upgrading from Free to Pro tiers removes significant roadblocks, shifting usage from occasional queries to a consistent workflow.",
            "Premium plans unlock advanced models (like GPT‑4 and Gemini 2.5 Pro) which provide far superior reasoning, coding, and analytical capabilities crucial for higher education.",
            "Features like large context windows (Claude, Gemini Ultra), deep web research (Gemini), and code execution (ChatGPT) enable innovative teaching and research methods not possible with free versions.",
            "For institutional rollout, Enterprise/Edu plans offer essential security, privacy, and management features, making them a worthwhile investment for fostering responsible AI use on campus.",
          ],
          icon: "Lightbulb",
        },
      ];

      // -----------------------------
      //  Helper – map icon name to JSX
      // -----------------------------
      const icons = {
        GraduationCap: <GraduationCap className="h-12 w-12 text-blue-500" />,
        Zap: <Zap className="h-12 w-12 text-yellow-500" />,
        Building: <Building className="h-12 w-12 text-gray-500" />,
        Bot: <Bot className="h-16 w-16 text-green-500" />,
        BrainCircuit: <BrainCircuit className="h-16 w-16 text-purple-500" />,
        BotMessageSquare: <BotMessageSquare className="h-16 w-16 text-orange-500" />,
        FileText: <FileText className="h-16 w-16 text-indigo-500" />,
        Lightbulb: <Lightbulb className="h-16 w-16 text-amber-400" />,
      };

      // -----------------------------
      //  Slide Components
      // -----------------------------
      const TitleSlide = ({ slide }) => (
        <div className="flex flex-col items-center justify-center text-center h-full p-8 bg-gray-900 rounded-lg">
          <div className="bg-blue-500 p-4 rounded-full mb-6">
            <Bot className="h-16 w-16 text-white" />
          </div>
          <h1 className="text-4xl md:text-5xl font-bold text-white leading-tight">
            {slide.title}
          </h1>
          <p className="mt-4 text-lg md:text-xl text-gray-300">{slide.subtitle}</p>
        </div>
      );

      const IntroSlide = ({ slide }) => (
        <div className="p-8 md:p-12 bg-gray-800 text-white rounded-lg h-full">
          <h2 className="text-3xl font-bold text-center mb-8">{slide.title}</h2>
          <div className="grid md:grid-cols-3 gap-6">
            {slide.points.map((point, i) => (
              <div
                key={i}
                className="bg-gray-700 p-6 rounded-lg shadow-lg flex flex-col items-center text-center"
              >
                <div className="mb-4">{icons[point.icon]}</div>
                <h3 className="text-xl font-semibold mb-2 text-blue-400">
                  {point.title}
                </h3>
                <p className="text-gray-300 text-sm">{point.content}</p>
              </div>
            ))}
          </div>
        </div>
      );

      const ToolSlide = ({ slide }) => (
        <div className="p-8 md:p-12 bg-gray-800 text-white rounded-lg h-full overflow-y-auto">
          <div className="flex items-center justify-center mb-6">
            {icons[slide.icon]}
            <h2 className="text-4xl font-bold ml-4">{slide.toolName}</h2>
          </div>
          <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-4">
            {slide.tiers.map((tier, idx) => (
              <div
                key={idx}
                className="bg-gray-700 p-4 rounded-lg shadow-lg flex flex-col"
              >
                <h3 className="text-xl font-bold text-blue-400">{tier.name}</h3>
                <p className="text-lg font-semibold text-gray-300 mb-3">
                  {tier.price}
                </p>
                <ul className="space-y-2 text-sm list-disc list-inside text-gray-300 flex-grow">
                  {tier.features.map((f, i2) => (
                    <li
                      key={i2}
                      dangerouslySetInnerHTML={{
                        __html: f.replace(/\*\*(.*?)\*\*/g, '<strong class="text-yellow-300">$1</strong>'),
                      }}
                    />
                  ))}
                </ul>
              </div>
            ))}
          </div>
          {slide.note && (
            <div className="mt-6 p-4 bg-indigo-900/50 rounded-lg border border-indigo-700">
              <p className="text-indigo-200 text-center text-sm">{slide.note}</p>
            </div>
          )}
        </div>
      );

      const ComparisonSlide = ({ slide }) => (
        <div className="p-4 md:p-8 bg-gray-800 text-white rounded-lg h-full overflow-x-auto">
          <h2 className="text-3xl font-bold text-center mb-6">{slide.title}</h2>
          <table className="w-full min-w-[600px] text-left border-collapse">
            <thead>
              <tr className="bg-gray-700">
                {slide.headers.map((h, i) => (
                  <th
                    key={i}
                    className="p-3 text-sm font-semibold text-blue-400 border-b-2 border-gray-600"
                  >
                    {h}
                  </th>
                ))}
              </tr>
            </thead>
            <tbody>
              {slide.rows.map((row, r) => (
                <tr key={r} className="bg-gray-800 hover:bg-gray-700/50">
                  {row.map((cell, c) => (
                    <td
                      key={c}
                      className={`p-3 text-sm border-b border-gray-600 ${
                        c === 0 ? "font-semibold text-gray-300" : "text-gray-400"
                      }`}
                    >
                      {cell}
                    </td>
                  ))}
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      );

      const ConclusionSlide = ({ slide }) => (
        <div className="p-8 md:p-12 bg-gray-800 text-white rounded-lg h-full flex flex-col items-center justify-center text-center">
          <div className="mb-6">{icons[slide.icon]}</div>
          <h2 className="text-3xl font-bold mb-6">{slide.title}</h2>
          <ul className="space-y-4 text-md text-gray-300 max-w-3xl list-disc list-inside text-left">
            {slide.points.map((p, i) => (
              <li key={i}>{p}</li>
            ))}
          </ul>
        </div>
      );

      // Helper to render a slide by type
      const renderSlide = (slide) => {
        switch (slide.type) {
          case 'title':      return <TitleSlide slide={slide} />;
          case 'intro':      return <IntroSlide slide={slide} />;
          case 'tool':       return <ToolSlide slide={slide} />;
          case 'comparison': return <ComparisonSlide slide={slide} />;
          case 'conclusion': return <ConclusionSlide slide={slide} />;
          default:           return <div className="p-8 text-white">Unknown slide</div>;
        }
      };

      // Main wrapper
      const App = () => {
        const [idx, setIdx] = React.useState(0);
        const next  = () => setIdx((i) => (i + 1) % presentationData.length);
        const prev  = () => setIdx((i) => (i - 1 + presentationData.length) % presentationData.length);
        const slide = presentationData[idx];

        return (
          <div className="bg-gray-900 text-white min-h-screen w-full flex flex-col items-center justify-center p-4">
            <div className="w-full max-w-6xl aspect-[16/9] bg-gray-800 rounded-xl shadow-2xl flex flex-col overflow-hidden">
              <div className="flex-grow p-2">
                {renderSlide(slide)}
              </div>

              <div className="flex-shrink-0 bg-gray-900/50 p-3 flex items-center justify-between border-t border-gray-700">
                <button onClick={prev} className="flex items-center px-4 py-2 bg-blue-600 hover:bg-blue-700 rounded-md">
                  <ChevronLeft className="h-5 w-5 mr-1" /> Prev
                </button>

                <span className="text-sm text-gray-400">Slide {idx + 1} of {presentationData.length}</span>

                <button onClick={next} className="flex items-center px-4 py-2 bg-blue-600 hover:bg-blue-700 rounded-md">
                  Next <ChevronRight className="h-5 w-5 ml-1" />
                </button>
              </div>
            </div>
          </div>
        );
      };

      // Mount React
      const rootEl = document.getElementById('root');
      const root = ReactDOM.createRoot(rootEl);
      root.render(<App />);
    }

    runWhenLibsAreReady();
  </script>
</body>
</html>
