---
title: PPM 電源制御コード
description: このトピックで説明されている電源制御コードは、プラットフォーム拡張機能プラグイン (Pep) によって使用されます。
ms.assetid: 4BA89D0F-78F0-44DF-BC9B-0F9F3256CD59
keywords:
- PPM 電源制御コード
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 11fdc731ded56ed58243887071f7504a49e79a2b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369136"
---
# <a name="ppm-power-control-codes"></a>PPM 電源制御コード

このトピックで説明されている電源制御コードは、プラットフォーム拡張機能プラグイン (Pep) によって使用されます。 電源制御要求は、I/O 制御要求 (IOCTL) に似ています。 IOCTL とは異なりただし、電源制御要求は、ウィンドウの電源管理フレームワーク (PoFx) に直接送信し、デバイス スタックの他のデバイス ドライバーでは発生しません。

次に、PPM の電源制御コードを示します。

|コード |構文 |説明 |
|---|---|---|
|PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE|<p> // {38BD8901-AB20-4908-ABAA-AC34674BDFF3}</p><p>DEFINE_GUID (PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE、 </p><p>0x38bd8901、0xab20、0x4908、0xab、0xaa、0xac、0x34、0x67、0x4b、0 xdf、0xf3)。</p>| PEP はコードを使用して、クエリ プロセッサに割り当てられているパーキング ページについて Windows の電源管理フレームワーク (PoFx) を実行します。 <p>プロセッサのパーキング ページを確認するのには、プラットフォームの拡張機能プラグイン (PEP) このプロセッサは、PoFx PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE power コントロール要求を送信します。</p> <p>この電源制御要求を開始するには、PEP はまず PoFx PEP に送信する作業項目を通知するために、RequestWorker ルーチンを呼び出します。 PoFx は、PEP へ PEP_DPM_WORK 通知を送信することによって、この呼び出しに応答します。 PEP はパーキング ページの情報の電源制御作業要求を送信して応答します。 この要求には、PEP に割り当てられた PEP_WORK_INFORMATION 構造体、作業の種類別のメンバーは PepWorkRequestPowerControl に設定し、PEP に割り当てられた PEP_WORK_POWER_CONTROL 構造体を指す PowerControl メンバーが含まれます。 PEP_WORK_POWER_CONTROL 構造体の PowerControlCode メンバーは、PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE に設定されます。 この構造体の InBuffer メンバーが NULL の場合し、OutBuffer メンバーは、PEP に割り当てられた PEP_PPM_CONTEXT_QUERY_PARKING_PAGE 構造体を指す必要があります。 この電源制御要求に応答して、PoFx はパーキング ページの仮想および物理アドレスが PEP_PPM_CONTEXT_QUERY_PARKING_PAGE 構造に書き込みを行います。</p><p>PEP_PPM_POWER_CONTROL_QUERY_PARKING_PAGE power のコントロール要求は ARM 固有であるため、x86 および x64 プロセッサでサポートされていません。 ARM マルチプロセッサ システムでは、パーキング ページは、オペレーティング システムがプロセッサがアイドル状態からの起動を制御するためのメールボックスとして使用するメモリのブロック 4 キロバイトです。 PEP は、メールボックスの一部を使用して、プロセッサ固有のコンテキスト データを格納する場合があります。 詳細については、「ARM プラットフォームのマルチプロセッサ スタートアップ」をという名前でドキュメントを参照してください。 https://www.acpica.org/related-documentsします。</p>|
|GUID_PPM_PERF_CONSTRAINT_CHANGE|<p> // {29181FA1-4BF3-4c2e-B314-A6D226322B00}</p><p>DEFINE_GUID (GUID_PPM_PERF_CONSTRAINT_CHANGE、</p><p>0x29181fa1, 0x4bf3, 0x4c2e, 0xb3, 0x14, 0xa6, 0xd2, 0x26, 0x32, 0x2b, 0x0);</p>|PEP はコードを使用して、Windows の電源管理を通知するには、外部の制約 (power 予算、温度の制約、電源、およびなど) に対応するために、プロセッサのパフォーマンスを制限するフレームワーク (PoFx) を変更する必要があります。 <p>この制御コードには、入力または出力バッファーは使用されません。</p><p>この電源制御要求を開始するには、PEP はまず PoFx PEP に送信する作業項目を通知するために、RequestWorker ルーチンを呼び出します。 PoFx は、PEP へ PEP_DPM_WORK 通知を送信することによって、この呼び出しに応答します。 PEP は、パフォーマンス制約の変更の電源制御作業要求を送信して応答します。 この要求には、PEP に割り当てられた PEP_WORK_INFORMATION 構造体、作業の種類別のメンバーは PepWorkRequestPowerControl に設定し、PEP に割り当てられた PEP_WORK_POWER_CONTROL 構造体を指す PowerControl メンバーが含まれます。 PEP_WORK_POWER_CONTROL 構造体の PowerControlCode メンバーは、GUID_PPM_PERF_CONSTRAINT_CHANGE に設定されます。 この構造体の InBuffer と OutBuffer の両方のメンバーは、NULL である必要があります。 この電源制御要求に応答して、PoFx は新しいプロセッサ パフォーマンスの制限値を取得する PEP に PEP_NOTIFY_PPM_PERF_CONSTRAINTS 通知を送信します。</p>
 

 

