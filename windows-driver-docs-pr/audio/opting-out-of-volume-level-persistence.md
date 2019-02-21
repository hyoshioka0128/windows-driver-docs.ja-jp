---
title: ボリューム レベルの持続性を無効にします。
description: ボリューム レベルの持続性を無効にします。
ms.assetid: e96533be-25e8-49ae-8e56-7105dfa92b5a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d5742006ae28e4a5db2166e674197e4f4ab0f29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549634"
---
# <a name="opting-out-of-volume-level-persistence"></a>ボリューム レベルの持続性を無効にします。


既定では、コンピューターを再起動するときに、ボリューム レベルの設定が維持されます。 この既定のシステム動作と呼びます*ボリュームの永続化*します。 コンピューターの再起動後に、システムに保持するボリューム レベルしたくない場合は、システムの既定の動作を無効にオーディオのアダプターのインストール時に、INF ファイルを使用できます。

ドライバー、ドライバーが、独自のレジストリのキャッシュとハードウェア自体、ドライバーの読み込み時に、レベルを設定する場合、ボリュームの永続化をオプトアウトすることができます。

INF ファイルを使用してボリュームの永続化を解除するには使用、 [ **AddProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff546318)鍵の値を設定するレジストリ ディレクティブ\_AudioDevice\_DontPersistControls レジストリ「1」にキー。 既定値は「0」です。

次の INF ファイル フラグメントは、ボリュームの永続化を無効にする方法を示します。

```inf
 
;; INF file fragment to show how to use AddProperty
;; to opt out of volume persistence
;;
[Version]
Signature = "$CHICAGO$"
Class = MEDIA
ClassGUID = {...}
...
[Manufacturer]
%MfgName% = CompanyName
...
[CompanyName]
%DeviceDescription% = HdAudModel, hw-id
;; ... other device models listed here

[HdAudModel]
Include=ks.inf, wdmaudio.inf
Needs=KS.Registration, WDMAUDIO.Registration
CopyFiles = HdAudModel.CopyList, HdAudProp.CopyList, HdAudShortCut.CopyList
AddReg = HdAudModel.AddReg, HdAudProp.AddReg, HdAudShortCut.AddReg, HdAudBranding.AddReg
AddProperty = HdAudModel.AddProperty
...
[HdAudModel.AddProperty]
;; {F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},2,7,,0
{F3E80BEF-1723-4FF2-BCC4-7F83DC5E46D4},2,7,,1
...
[Strings]
MfgName = "My Company Name Inc"
DeviceDescription = "My WDM device driver"
```

**注**  のみ、上記の INF ファイルのフラグメントが表示されます、**バージョン**セクションと関連するセクションで、 [ **AddProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff546318)ディレクティブ。

 

**% MfgName CompanyName =** 内のエントリの行、**製造元**セクション参照、 **CompanyName**セクション where オーディオのアダプターのモデルとハードウェア ID (hw id)提供されます。 このセクションで、モデルとハードウェア id の情報が提供されている、INF ファイルと呼びます、*セクションをモデル化*します。 セクションの実際のタイトルでは、ユーザーが定義し、前の例では**CompanyName**します。 INF ファイルのモデルのセクションの詳細については、次を参照してください。 [ **INF モデル セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)します。

モデルのセクションは、さらに、セットアップ プログラムをコピーする必要があるその他の INF ファイルに関する情報を提供する場所、デバイス ドライバー インストール (DDInstall) セクションを参照します。 このセクションの実際のタイトルでは、ユーザーが定義し、前の例では**HdAudModel**します。 **KS を = 必要があります。登録しています.** 行のエントリのインストールについては、セットアップ プログラムを取得する必要があります、INF ファイル内で特定のセクションでは、データを提供

**HdAudModel**セクションにも、AddReg および AddProperty セクションへの参照が含まれています。 セットアップ プログラムは、それぞれのレジストリ キーとデバイスのプロパティを設定するには、AddReg と AddProperty からデータを取得します。 ここで参照されて AddProperty セクションは**HdAudModel.AddProperty**デバイス プロパティ情報を提供する、次の形式を使用しています。

{*property-category-guid*}, *property-pid*, *type*, \[*flags*\], *value*

**HdAudModel**セクションがコメント アウトされた最初のものの 2 つの行エントリを示しています。コメント アウトされている行のエントリが「1」にデバイス プロパティの値を設定します。 コメント アウトされていない行のエントリは、セットアップ プログラムを読み取ります。 この行のエントリが「0」に設定するデバイスのプロパティの値 このデバイスのプロパティが「0」に設定されている場合、オーディオ デバイス ボリュームの永続化からオプトアウトします。

AddProperty ディレクティブの詳細については、次を参照してください。 [ **INF AddProperty ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546318)します。

上記の INF ファイルのコードでプロパティ カテゴリ GUID およびプロパティ ID に対応するプロパティ名が鍵\_AudioDevice\_DontPersistControls します。

 

 




