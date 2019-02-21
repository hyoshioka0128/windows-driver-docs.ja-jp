---
title: Windows での UEFI
description: Windows での UEFI
ms.assetid: 14b54fe3-49f7-4ad8-b9b6-ecc747dff137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73ce63723ac4fa81625b634647792edc18062b5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538835"
---
# <a name="uefi-in-windows"></a>Windows での UEFI


**注**  このセクションの一部の情報は、Windows 10 Mobile と特定のプロセッサ アーキテクチャにのみ適用可能性があります。

 

Windows、Unified Extensible Firmware インターフェイス (UEFI) システムの制御、SoC ファームウェア ブート ローダーから OS のハンドオフをサポートするために使用します。 UEFI 環境では、Windows デバイスを起動すると、OS と OS が実行される最小限のブートが。

UEFI は、標準環境およびプラットフォームのファームウェア ブート オペレーティング システムを許可するためのインターフェイスのセットを記述する標準の UEFI 仕様に基づくブート ローダーの一般的なフレームワークです。 UEFI 仕様については、「 [ http://uefi.org/specifications](https://go.microsoft.com/fwlink/p/?LinkId=218221)します。 UEFI の非常に低レベル性質上、その実装の特定 SoC. に固有です。 Windows デバイスの場合、コアの UEFI 環境と一部の UEFI ドライバーが SoC ベンダーによって提供されます。 UEFI ドライバーと点滅アプリケーションの場合) などの UEFI アプリケーションは、Microsoft によって提供されます。

だけでなく、UEFI 仕様に記載されている実装の詳細は、SoC プラットフォームで Windows を実行するための UEFI 要件のセットを追加します。 これらの要件を参照してください。 [SoC プラットフォームで Windows の最小の UEFI 要件](minimum-uefi-requirements-for-windows-on-soc-platforms.md)します。

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
<td><p><a href="minimum-uefi-requirements-for-windows-on-soc-platforms.md" data-raw-source="[Minimum UEFI requirements for Windows on SoC platforms](minimum-uefi-requirements-for-windows-on-soc-platforms.md)">SoC のプラットフォームで Windows の最小の UEFI 要件</a></p></td>
<td><p>統一された Extensible Firmware Interface (UEFI) では、Windows を実行している SoC プラットフォームの必要なブート ファームウェアです。 このセクションでは、SoC プラットフォームで Windows を実行するための UEFI の実装要件について説明します。 監視とこれらの要件への準拠により、Windows の適切な機能を保証は役立ちます。</p></td>
</tr>
<tr class="even">
<td><p><a href="uefi-protocols-for-windows.md" data-raw-source="[UEFI protocols for Windows](uefi-protocols-for-windows.md)">Windows の UEFI プロトコル</a></p></td>
<td><p>このセクションでは、Windows によって定義されている UEFI プロトコルについて説明します。 これらのプロトコルは、UEFI 仕様で定義されたプロトコルでの展開し、ブート プロセス中に特定の関数を実行する Windows で使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="windows-uefi-firmware-update-platform.md" data-raw-source="[Windows UEFI firmware update platform](windows-uefi-firmware-update-platform.md)">Windows の UEFI ファームウェアを更新するプラットフォーム</a></p></td>
<td><p>Windows では、インストールを実行するシステムとドライバー パッケージは、UEFI UpdateCapsule 関数を使用して処理を使用してデバイス ファームウェアの更新プログラム、プラットフォームをサポートしています。 このプラットフォームにより、一貫性、信頼性の高いファームウェアの更新プログラムのエクスペリエンスとエンドユーザー向けの重要なシステム ファームウェアの更新プログラムの見つけやすさが向上します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="uefi-components-for-windows"></a>Windows の UEFI コンポーネント


次の図は、Windows デバイスの主な UEFI コンポーネントを示しています。

![windows phone 用の uefi コンポーネント](images/oem-uefi-components.png)

## <a name="oem-components-in-the-uefi-environment"></a>UEFI 環境で OEM コンポーネント


Oem は、製造とデバイスのサービスで支援する UEFI アプリケーションを追加できます。 これらのアプリケーションをエンドユーザーにアクセスすることはできません。 エンドユーザー向けの UEFI アプリケーションは Microsoft によってのみ実装し、Windows ブート マネージャーを起動します。

UEFI アプリケーションを実装する Oem は、小さなできるだけのメモリ フット プリントし、さらにブート時に影響しないことを確認してください。 UEFI 環境のコンポーネントの作成の詳細については、SoC 仕入先を参照してください。

**重要な**   Oem は、その特定のハードウェアに合わせて SoC ベンダーから提供される特定の UEFI ドライバーを置き換える場合にも必要があります。 詳細については、SoC ベンダーを補足します。

 

## <a name="related-topics"></a>関連トピック
[Windows の UEFI プロトコル](uefi-protocols-for-windows.md)  



