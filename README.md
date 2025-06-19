import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Coffee, IceCream, CoffeeCup } from "lucide-react";

export default function CafeKiosk() {
  const [step, setStep] = useState(0);
  const [menu, setMenu] = useState("");
  const [temp, setTemp] = useState("");

  const handleMenuClick = (item: string) => {
    setMenu(item);
    setStep(1);
  };

  const handleTempClick = (temperature: string) => {
    setTemp(temperature);
    setStep(2);
  };

  const handleRestart = () => {
    setStep(0);
    setMenu("");
    setTemp("");
  };

  const renderStep = () => {
    if (step === 0) {
      return (
        <div className="grid gap-4">
          <h2 className="text-xl font-bold">음료를 선택해주세요 (Choose a drink)</h2>
          <Button variant="default" className="bg-blue-500 text-white" onClick={() => handleMenuClick("아메리카노 Americano")}>
            <Coffee className="inline mr-2" /> 아메리카노 Americano
          </Button>
          <Button variant="default" className="bg-green-500 text-white" onClick={() => handleMenuClick("카페라떼 Cafe Latte")}>
            <CoffeeCup className="inline mr-2" /> 카페라떼 Cafe Latte
          </Button>
          <Button variant="default" className="bg-yellow-500 text-white" onClick={() => handleMenuClick("바닐라라떼 Vanilla Latte")}>
            <IceCream className="inline mr-2" /> 바닐라라떼 Vanilla Latte
          </Button>
        </div>
      );
    } else if (step === 1) {
      return (
        <div className="grid gap-4">
          <h2 className="text-xl font-bold">{menu} - 따뜻하게 드릴까요, 차갑게 드릴까요?</h2>
          <Button className="bg-red-500 text-white" onClick={() => handleTempClick("HOT")}>🔥 HOT</Button>
          <Button className="bg-cyan-500 text-white" onClick={() => handleTempClick("ICE")}>❄️ ICE</Button>
        </div>
      );
    } else if (step === 2) {
      return (
        <Card>
          <CardContent className="p-4 space-y-2 text-lg">
            <p>1. {menu} {temp} 주문받았습니다.<br />1. {menu} {temp} order received.</p>
            <p>2. 선생님 성함을 알려주세요.<br />2. May I have your name, please?</p>
            <p>3. 잠시만 앉아서 기다려 주세요.<br />3. Please have a seat and wait a moment.</p>
            <Button className="mt-4 bg-gray-700 text-white" onClick={handleRestart}>처음으로 (Start Over)</Button>
          </CardContent>
          <CardContent className="mt-4 text-sm text-gray-600">
            <p><strong>주문 내역:</strong> {menu} ({temp})</p>
          </CardContent>
        </Card>
      );
    }
  };

  return (
    <div className="p-6 max-w-md mx-auto space-y-6">
      <h1 className="text-2xl font-bold text-center">꿈나래반 모의카페 주문</h1>
      {renderStep()}
    </div>
  );
}
