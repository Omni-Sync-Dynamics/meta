
```latex
\documentclass[11pt,a4paper]{article}

% --- Packages ---
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[margin=1in]{geometry}
\usepackage{titlesec}
\usepackage{tabularx}
\usepackage{booktabs}
\usepackage[table]{xcolor}
\usepackage{hyperref}
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{caption}

% --- Color Definitions ---
\definecolor{riskLow}{HTML}{90EE90} % Green
\definecolor{riskMed}{HTML}{FFFFE0} % Yellow
\definecolor{riskHigh}{HTML}{FFD580} % Orange
\definecolor{riskExt}{HTML}{FF7F7F} % Red
\definecolor{headerGray}{HTML}{EFEFEF}

% --- Custom Commands ---
\newcommand{\riskLevel}[1]{%
    \ifnum#1<5 \cellcolor{riskLow}Low \else
    \ifnum#1<10 \cellcolor{riskMed}Medium \else
    \ifnum#1<15 \cellcolor{riskHigh}High \else
    \cellcolor{riskExt}Extreme \fi\fi\fi
}

% --- Document Info ---
\title{\textbf{Manipulator Subsystem: Risk Assessment Report}\\ 
\large Mechatronics Omni-Challenge - Spring 2026}
\author{Subsystem: Arm / Manipulator Module}
\date{\today}

\begin{document}

\maketitle

\section{Introduction}
This document outlines the risk assessment process and results for the Manipulator Subsystem of the Modular Omni-Wheel Mobile Manipulator. The goal of this Failure Mode and Effects Analysis (FMEA) style report is to proactively identify, analyze, and evaluate potential mechanical, electrical, software, and perception risks to minimize their negative impact on project performance, safety, and competition constraints.

\section{Risk Assessment Matrix}
The risk score $R$ is calculated by the product of Likelihood ($L$) and Impact ($I$):
\begin{equation}
    R = L \times I
\end{equation}

\noindent Priority is determined by the following scale:

\begin{center}
\begin{tabularx}{\textwidth}{|c|X|c|X|c|l|}
\hline
\rowcolor{headerGray}
\textbf{L} & \textbf{Description} & \textbf{I} & \textbf{Description} & \textbf{Score (R)} & \textbf{Risk Level} \\ \hline
1 & Rare & 1 & Insignificant & 1 -- 4 & \cellcolor{riskLow} Low \\ \hline
2 & Unlikely & 2 & Minor & 5 -- 9 & \cellcolor{riskMed} Medium \\ \hline
3 & Moderate & 3 & Moderate & 10 -- 14 & \cellcolor{riskHigh} High \\ \hline
4 & Likely & 4 & Major & 15 -- 20 & \cellcolor{riskExt} Extreme \\ \hline
5 & Almost Certain & 5 & Catastrophic & 21 -- 25 & \cellcolor{riskExt} Extreme \\ \hline
\end{tabularx}
\end{center}

\section{Identified Risks and Mitigation Strategies}

\subsection{Mechanical Risks (M)}
Focuses on physical structure, spatial constraints, and gripper dynamics.

\begin{tabularx}{\textwidth}{|l|X|c|c|c|l|X|}
\hline
\rowcolor{headerGray}
\textbf{ID} & \textbf{Risk Description} & \textbf{L} & \textbf{I} & \textbf{R} & \textbf{Level} & \textbf{Mitigation Strategy} \\ \hline
M-001 & Arm tip deflection/oscillation & 4 & 3 & 12 & \riskLevel{12} & Use carbon fiber; S-curve profiling. \\ \hline
M-002 & Base joint mechanical failure & 2 & 5 & 10 & \riskLevel{10} & Use thrust bearings; metal brackets. \\ \hline
M-003 & Exceeding dimension constraints & 2 & 5 & 10 & \riskLevel{10} & Foldable kinematic chain; Week 3 CAD check. \\ \hline
M-005 & Wire tangling or snapping & 4 & 4 & 16 & \riskLevel{16} & Internal routing; drag chains; silicone wire. \\ \hline
\end{tabularx}



\subsection{Electromechanical Risks (E)}
Concerns the intersection of control and physical output (torque/thermals).

\begin{tabularx}{\textwidth}{|l|X|c|c|c|l|X|}
\hline
\rowcolor{headerGray}
\textbf{ID} & \textbf{Risk Description} & \textbf{L} & \textbf{I} & \textbf{R} & \textbf{Level} & \textbf{Mitigation Strategy} \\ \hline
E-001 & Motors undersized for reach & 3 & 5 & 15 & \riskLevel{15} & Static torque calcs; counterweights. \\ \hline
E-002 & Actuator overheating (static) & 3 & 4 & 12 & \riskLevel{12} & Current reduction; worm gears. \\ \hline
E-003 & Gearbox backlash & 4 & 3 & 12 & \riskLevel{12} & Planetary gears; absolute output encoders. \\ \hline
\end{tabularx}

\subsection{Electrical \& Power Risks (P)}
Concerns power distribution and signal integrity.

\begin{tabularx}{\textwidth}{|l|X|c|c|c|l|X|}
\hline
\rowcolor{headerGray}
\textbf{ID} & \textbf{Risk Description} & \textbf{L} & \textbf{I} & \textbf{R} & \textbf{Level} & \textbf{Mitigation Strategy} \\ \hline
P-001 & MCU Brownout on high load & 4 & 5 & 20 & \riskLevel{20} & Isolate logic/motor rails; bypass caps. \\ \hline
P-003 & Signal noise (I2C/SPI) & 4 & 4 & 16 & \riskLevel{16} & Twisted pairs; shielded cables; CAN bus. \\ \hline
\end{tabularx}

\subsection{Software \& Control Risks (S)}
Concerns kinematics, safety states, and communication.

\begin{tabularx}{\textwidth}{|l|X|c|c|c|l|X|}
\hline
\rowcolor{headerGray}
\textbf{ID} & \textbf{Risk Description} & \textbf{L} & \textbf{I} & \textbf{R} & \textbf{Level} & \textbf{Mitigation Strategy} \\ \hline
S-001 & Self-collision/Hard stops & 3 & 5 & 15 & \riskLevel{15} & Software limits; physical limit switches. \\ \hline
S-003 & Comms timeout (Heartbeat) & 3 & 4 & 12 & \riskLevel{12} & 10Hz ping; safe-state motor freeze. \\ \hline
\end{tabularx}

\subsection{Perception Risks (C)}
Integration of sensors and QR vision systems.

\begin{tabularx}{\textwidth}{|l|X|c|c|c|l|X|}
\hline
\rowcolor{headerGray}
\textbf{ID} & \textbf{Risk Description} & \textbf{L} & \textbf{I} & \textbf{R} & \textbf{Level} & \textbf{Mitigation Strategy} \\ \hline
C-001 & QR lighting/shadow failure & 3 & 5 & 15 & \riskLevel{15} & Active LED ring; auto-exposure pipeline. \\ \hline
C-002 & Gripper obstructs camera FOV & 4 & 4 & 16 & \riskLevel{16} & FOV modeling in CAD; offset mounting. \\ \hline
\end{tabularx}

\end{document}
```