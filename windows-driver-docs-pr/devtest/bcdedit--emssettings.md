---
title: BCDEdit/emssettings
description: /Emssettings オプションは、コンピューターのグローバルの緊急管理サービス (EMS) の設定を設定します。 を有効にまたは EMS を無効にするには、/ems オプションを使用します。 /Emssettings オプションを有効または任意のブート エントリの EMS を無効にするにはありません。
ms.assetid: 010e852d-ff97-4280-b35b-f1881e249e42
ms.date: 07/03/2018
keywords:
- BCDEdit/emssettings ドライバー開発ツール
topic_type:
- apiref
api_name:
- BCDEdit /emssettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 18757cc3041b8e5673218516f4368a083892f502
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531444"
---
# <a name="bcdedit-emssettings"></a>BCDEdit/emssettings


**/Emssettings**オプションは、コンピューターのグローバルの緊急管理サービス (EMS) の設定を設定します。 有効または EMS を無効にする、使用、 **/ems**オプション。 **/Emssettings**オプションも有効または任意のブート エントリの EMS を無効にします。

構文 

```
    bcdedit /emssettings [ BIOS ] | [ EMSPORT: port | [EMSBAUDRATE: baudrate] ] 
```

<a name="parameters"></a>パラメーター
----------

**BIOS**   
システムが BIOS 設定を使用して EMS 構成のことを指定します。 これは、BIOS によって提供される EMS サポートしているシステムでのみ機能します。

 **EMSPORT:** *ポート*   
EMS のポートとして使用するシリアル ポートを指定します。 このパラメーターを指定しないで、 **BIOS**オプション。

**EMSBAUDRATE:** *baudrate*   
EMS を使用するシリアル ボー レートを指定します。 このコマンドは、BIOS で指定されていませんする必要があります。 *Baudrate*は省略可能で、既定値は 9,600 bps です。

### <a name="comments"></a>コメント

正しく Windows をインストールした後は、EMS のコンソールのリダイレクトを有効に、Windows のコンピューターで帯域外通信に使用されるポートと送信レートを把握する必要があります。 Windows では、EMS のコンソールのリダイレクトをこれらの同じ設定を使用します。

コンピューターの BIOS ファームウェアと ACPI シリアル ポート Console Redirection (SPCR) テーブルでは、Windows は SPCR テーブル内のエントリを読み取ることで、BIOS で確立された帯域外の設定を確認できます。 これらのシステムで使用することができます、 **BIOS**ポートの設定の SPCR テーブルで検索する Windows に出力するためのパラメーターを使用できる、 **emsport:**<em>ポート</em>と**emsbaudrate:**<em>baudrate</em> SPCR テーブルの設定を上書きするパラメーター。

BIOS ファームウェア、SPCR テーブルにはありませんがいるコンピューターで、BCDEdit を使用して、 **/emssettings**コマンドと、 **emsport:**<em>ポート</em>ポートを指定するパラメーターと**emsbaudrate:**<em>baudrate</em>転送速度を指定するパラメーター。

すべてのシステムで使用して、 [ **BCDEdit/ems** ](bcdedit--ems.md)コマンドし、ブート エントリが読み込まれるオペレーティング システムで EMS のコンソール リダイレクトを有効にするブート エントリを指定します。

このセクションで説明されているブート パラメーターでは、Windows のインストール後に、EMS のコンソールのリダイレクトが有効にします。 新規インストールまたは Windows のアップグレード中に、EMS を有効にする方法についてで「を有効にする緊急管理サービス」の検索、 [Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=10111) web サイト。

詳細の例では、次を参照してください。 [EMS のリダイレクトを有効にするのにブート パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff542282)します。

 

 





