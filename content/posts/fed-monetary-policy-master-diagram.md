---
title: "연준 통화정책 마스터 다이어그램"
date: 2026-03-16
tags: ["Economics", "Fed", "Monetary Policy"]
summary: "연준의 금리 정책, 대차대조표 정책, 시장 참여자, 유동성, 그리고 피드백 루프까지 하나의 다이어그램으로 정리합니다."
mermaid: true
---

## 연준 통화정책의 전체 구조

연준(Federal Reserve)의 통화정책은 크게 **금리 정책**(간접 조정)과 **대차대조표 정책**(직접 조정)으로 나뉩니다. 이 두 축이 연준의 부채 계정들, 시장 참여자들, 그리고 시장 유동성과 금리에 어떻게 연결되는지를 하나의 다이어그램으로 정리해 보았습니다.

```mermaid
graph TB
    subgraph POLICY["연준 통화정책"]
        FED["연준<br/>Federal Reserve"]

        subgraph RATE_POLICY["금리 정책 간접조정"]
            IOER["IOER 금리<br/>지준금 이자율<br/>상한 역할"]
            ONRRP["ON RRP 금리<br/>역레포 이자율<br/>하한 역할"]
        end

        subgraph BALANCE_POLICY["대차대조표 정책 직접조정"]
            QE["QE/QT<br/>양적완화/긴축<br/>자산 직접 매입/매각"]
        end
    end

    subgraph FED_ASSETS["연준 대차대조표 자산측"]
        ASSETS["SOMA 자산<br/>국채 + MBS"]
    end

    subgraph FED_LIABILITIES["연준 대차대조표 부채측"]
        RESERVE["지준금 계정<br/>Reserve Balances<br/>은행 예치금"]
        RRP["역레포 계정<br/>ON RRP Facility<br/>MMF/GSE 예치금"]
        TGA["재무부 계정<br/>TGA<br/>Treasury General Account"]
    end

    subgraph PARTICIPANTS["시장 참여자"]
        BANK["상업은행<br/>Commercial Banks"]
        MMF["머니마켓펀드<br/>Money Market Funds"]
        GSE["GSE 등"]
        TREASURY["미 재무부<br/>US Treasury"]
    end

    MARKET_LIQ["시장 유동성<br/>Market Liquidity"]
    MARKET_RATE["시장금리<br/>Fed Funds Rate 등"]

    subgraph FEEDBACK_LOOP["정책 피드백 순환"]
        WATCH["시장 관찰<br/>Daily Monitoring"]
        ASSESS["효과 평가<br/>vs 목표"]
    end

    %% 정책 설정
    FED -->|금리 설정| IOER
    FED -->|금리 설정| ONRRP
    FED -->|직접 실행| QE

    %% QE/QT 효과 (자산측 → 부채측)
    QE ==>|자산 직접 매입/매각| ASSETS
    ASSETS ==>|대차대조표 균형<br/>지준금 자동 증감| RESERVE
    ASSETS -.->|RRP 거래의<br/>국채 담보 제공| RRP

    %% 금리정책의 유인효과
    IOER -.->|금리 수준에 따라<br/>예치/인출 유인| RESERVE
    ONRRP -.->|금리 수준에 따라<br/>예치/인출 유인| RRP

    %% 참여자와 연준 계정 간 관계 (현금 흐름)
    BANK <-->|현금 예치/인출<br/>예치금에 IOER 이자| RESERVE
    MMF <-->|현금 예치/인출<br/>예치금에 ON RRP 이자| RRP
    GSE <-->|현금 예치/인출<br/>예치금에 ON RRP 이자| RRP
    TREASURY <-->|정부 자금 예치/지출<br/>세금/국채발행/지출| TGA

    %% 연준 계정과 시장 유동성
    RESERVE -.->|은행 인출/활용시<br/>유동성 공급| MARKET_LIQ
    RRP <-.->|잔고 증가시 유동성 흡수<br/>잔고 감소시 유동성 공급| MARKET_LIQ
    TGA <-.->|잔고 증감에 따라<br/>유동성 흡수/공급| MARKET_LIQ

    %% 시장 금리 형성
    MARKET_LIQ -->|수요공급으로<br/>금리 형성| MARKET_RATE
    IOER -.->|상한선 제공| MARKET_RATE
    ONRRP -.->|하한선 제공| MARKET_RATE

    %% 피드백 루프
    MARKET_RATE -->|실효금리 관찰| WATCH
    MARKET_LIQ -->|유동성 상황 관찰| WATCH
    WATCH --> ASSESS
    ASSESS -->|정책 조정 필요시| FED

    classDef policyStyle fill:#e1f5ff,stroke:#0066cc,stroke-width:3px
    classDef assetStyle fill:#d4edda,stroke:#28a745,stroke-width:2px
    classDef liabilityStyle fill:#fff3cd,stroke:#ffc107,stroke-width:2px
    classDef participantStyle fill:#f8d7da,stroke:#dc3545,stroke-width:2px
    classDef marketStyle fill:#e2d5f0,stroke:#6f42c1,stroke-width:3px
    classDef rateStyle fill:#ffd6cc,stroke:#ff6b35,stroke-width:3px
    classDef feedbackStyle fill:#f0e6ff,stroke:#8b5cf6,stroke-width:2px

    class POLICY,FED,RATE_POLICY,BALANCE_POLICY,IOER,ONRRP,QE policyStyle
    class FED_ASSETS,ASSETS assetStyle
    class FED_LIABILITIES,RESERVE,RRP,TGA liabilityStyle
    class PARTICIPANTS,BANK,MMF,GSE,TREASURY participantStyle
    class MARKET_LIQ marketStyle
    class MARKET_RATE rateStyle
    class FEEDBACK_LOOP,WATCH,ASSESS feedbackStyle
```

## 핵심 구조 요약

### 두 가지 정책 축

- **금리 정책 (간접 조정)**: IOER과 ON RRP 금리를 설정하여 시장금리의 상한과 하한을 형성합니다. 시장 참여자들이 자발적으로 반응하도록 유인하는 간접적인 방식입니다.
- **대차대조표 정책 (직접 조정)**: QE/QT를 통해 국채와 MBS를 직접 매입하거나 매각합니다. 이는 연준 대차대조표의 자산측을 변동시키고, 부채측(지준금)이 자동으로 따라 움직입니다.

### 연준 대차대조표의 부채측 3대 계정

| 계정 | 참여자 | 유동성 효과 |
|------|--------|------------|
| **지준금 (Reserve Balances)** | 상업은행 | 은행이 인출/활용 시 시장에 유동성 공급 |
| **역레포 (ON RRP)** | MMF, GSE | 잔고 증가 = 유동성 흡수, 감소 = 유동성 공급 |
| **TGA** | 미 재무부 | 세금 징수/국채 발행 시 흡수, 정부 지출 시 공급 |

### 피드백 루프

연준은 실효 연방기금금리(EFFR)와 시장 유동성 상황을 매일 관찰하며, 목표 대비 괴리가 발생하면 금리 조정 또는 공개시장조작을 통해 정책을 미세 조정합니다.
