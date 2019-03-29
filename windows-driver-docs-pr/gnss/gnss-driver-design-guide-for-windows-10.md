---
title: Windows 10 用 GNSS ドライバー設計ガイド
description: Windows 10 で収束 Windows 場所スタックの GNSS (UMDF 2.0) の設計の要件とユニバーサル Windows ドライバーのアーキテクチャを説明します。
ms.assetid: FD8503DC-A43F-43B2-A1E9-D80778E326F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f1bcc473217f096d655dadd3be7ba9d80f6e7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579589"
---
# <a name="gnss-driver-design-guide-for-windows-10"></a>Windows 10 用 GNSS ドライバー設計ガイド


このガイドは、ユニバーサル Windows ドライバーのアーキテクチャと設計を Windows 10 で収束 Windows 場所スタックの GNSS (UMDF 2.0) を説明します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="gnss-driver-overview.md" data-raw-source="[GNSS driver overview](gnss-driver-overview.md)">GNSS ドライバーの概要</a></p></td>
<td><p>実装する方法については、GNSS ドライバー設計のガイドを使用して、 <strong>DeviceIoControl</strong> GNSS ドライバーを使用した Api GNSS アダプターなどの高レベルのオペレーティング システム コンポーネント (HLOS) が必要な GNSS 機能にアクセスできるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="gnss-driver-requirements.md" data-raw-source="[GNSS driver requirements](gnss-driver-requirements.md)">GNSS ドライバーの要件</a></p></td>
<td><p>Windows 10 用 GNSS ドライバーを開発する際に考慮すべき要件、前提条件、および制約について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="gnss-driver-architecture.md" data-raw-source="[GNSS driver architecture](gnss-driver-architecture.md)">GNSS ドライバーのアーキテクチャ</a></p></td>
<td><p>GNSS UMDF 2.0 ドライバーのアーキテクチャ、I/O の考慮事項の概要を説明し、セッションの追跡と修正プログラムのいくつかの型について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="gnss-driver-design.md" data-raw-source="[GNSS driver design](gnss-driver-design.md)">GNSS ドライバーの設計</a></p></td>
<td><p>データ構造体、エラー報告、およびドライバーのバージョン管理を含む Windows 10 用 GNSS ドライバーの開発時に考慮する設計原則について説明します。</p></td>
</tr>
</tbody>
</table>

 

 

 




