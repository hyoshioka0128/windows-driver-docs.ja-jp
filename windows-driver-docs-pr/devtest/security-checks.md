---
title: セキュリティの検査
description: セキュリティの検査
ms.assetid: fca92bad-7bb8-4a30-b303-48fd54c20c42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8b741fdb923958895f5ed46e5264b6feb6cf718
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378289"
---
# <a name="security-checks"></a>セキュリティの検査


Driver Verifier のセキュリティ チェックのオプションは、セキュリティの脆弱性につながる一般的なエラー用のドライバーを監視します。 このオプションは、以降 Windows Vista で使用できます。

具体的には、セキュリティ チェックのオプションは、次の不適切なドライバーの動作を探します。

- **パラメーターとして、ユーザー モードのアドレスを持つカーネル ZwXxx ルーチンを呼び出しています。** ドライバーを呼び出すいずれかと**Zw * Xxx*** ルーチン、Driver Verifier は、ユーザー モードのアドレスにはパラメーターがないことを確認します。 呼び出す場合**Zw * Xxx*** ルーチンでは、現在 KPROCESSOR\_モードになりが**kernelmode である**ルーチンがカーネル モード アドレスのように扱われることに、パラメーターが渡されます。 そのため、ドライバーがアプリケーションから受信したすべてのユーザー モード バッファーをプローブし、カーネルを呼び出す前に (たとえば、プール ブロックやデータ構造で、カーネル スタックに割り当て) のカーネル モード メモリに配置する必要があります**Zw * Xxx***ルーチンです。 ドライバーのパラメーターとしてユーザー モード バッファーではなく、キャプチャされたバッファーを使用する必要があります、 **Zw * Xxx*** ルーチン。

- **形式が正しくない UNICODE を使用したカーネル ZwXxx ルーチンを呼び出す\_パラメーターとして文字列。** ドライバーを呼び出すいずれかと**Zw * Xxx*** Driver Verifier チェックの UNICODE であるすべてのパラメーターを日常的な\_文字列値。 このような文字列で、Driver Verifier によって検出された一般的なエラーは次のとおりです。
  -   **バッファー フィールドは、ユーザー モードのメモリを指します。**
  -   **長さまたは MaximumLength パラメーターが正しくありません。** たとえば、 *MaximumLength* &lt; *長さ*します。 または、奇数をこれらの値の 1 つまたは両方。 Unicode 文字列を表すために使用するバイト数を表すためにもこれらの値のどちらも常にあります。
- **正しくないオブジェクトとカーネル ZwXxx ルーチンを呼び出す\_をパラメーターとして、属性の構造体。** ドライバーを呼び出すいずれかと**Zw * Xxx*** Driver Verifier チェック オブジェクトであるすべてのパラメーターを日常的な\_属性の構造体。 各オブジェクトのメンバー\_属性の構造体のパラメーターの対象のユーザー モード アドレスと UNICODE の同じチェック\_上記で説明する文字列値。

- **一貫性のない Irp-&gt;requestormode でや I/O 要求のパラメーター。** たびに、 **Irp -&gt; requestormode で**に設定されている**kernelmode である**、Driver Verifier は、ことを確認、I/O 要求パラメーターのない**Irp-&gt;AssociatedIrp.SystemBuffer**または**Irp -&gt;UserBuffer**はユーザー モード アドレスです。

Driver Verifier 以降、Windows 7 では、Driver Verifier のオプションを有効にすると、次のドライバーの動作を確認します。

**オブジェクトの参照カウンターは、0 から 1 に変更します。**
Windows カーネル オブジェクト マネージャーは、ファイル オブジェクトまたはスレッド オブジェクトなどのオブジェクトを作成するときに、新しいオブジェクトの参照カウンターが 1 に設定されます。 などのシステム関数を呼び出し[ **ObReferenceObjectByPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)または[ **ObReferenceObjectByHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)インクリメントの参照カウンター。 すべての呼び出しに[ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)参照カウンターをデクリメントのオブジェクトと同じです。

参照カウンターには、値 0 に達すると、オブジェクトが解放する対象となります。 オブジェクト マネージャーが、すぐに解放可能性があるか、後では無料可能性があります。 Driver Verifier は、後続の呼び出しをチェック[ **ObReferenceObjectByPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)と[ **ObReferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)同じオブジェクトに対して。 これらの呼び出しでは、0 から 1 で、ドライバーが既に解放されたオブジェクトの参照カウンターをインクリメントに参照カウンターを変更します。 これは常に他のメモリ割り当てが破損していることができます。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して 1 つまたは複数のドライバーのセキュリティ チェックのオプションをアクティブ化することができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインを使用**

    によって表されるセキュリティ チェックのオプションをコマンドラインで**ビット 8 (0x100)** します。 セキュリティ チェックを有効にするには、0x100 のフラグの値を使用して、または 0x100 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x100 /driver MyDriver.sys
    ```

    オプションは、コンピューターを再起動した後にアクティブになります。

    以降 Windows Vista では、することができますもアクティブ化および非アクティブ化のセキュリティ チェックを追加して、コンピューターを再起動しなくても、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x100 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    セキュリティ チェックのオプションは、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**、順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択**セキュリティ チェック**します。

    セキュリティ チェック機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーを使用する をクリックして**標準設定の作成**です。

 

 





