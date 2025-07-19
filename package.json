import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Card, CardContent } from "@/components/ui/card";

function generateRoundRobin(players) {
  const n = players.length;
  const rounds = [];
  const even = n % 2 === 0;
  const playerList = even ? [...players] : [...players, "Bye"];
  const numRounds = playerList.length - 1;
  const half = playerList.length / 2;

  for (let r = 0; r < numRounds; r++) {
    const round = [];
    for (let i = 0; i < half; i++) {
      const p1 = playerList[i];
      const p2 = playerList[playerList.length - 1 - i];
      if (p1 !== "Bye" && p2 !== "Bye") {
        if ((r + i) % 2 === 0) round.push({ white: p1, black: p2 });
        else round.push({ white: p2, black: p1 });
      }
    }
    playerList.splice(1, 0, playerList.pop());
    rounds.push(round);
  }
  return rounds;
}

export default function ChessScheduler() {
  const [players, setPlayers] = useState([]);
  const [nameInput, setNameInput] = useState("");
  const [rounds, setRounds] = useState([]);

  const addPlayer = () => {
    if (nameInput.trim() && !players.includes(nameInput)) {
      setPlayers([...players, nameInput.trim()]);
      setNameInput("");
    }
  };

  const startTournament = () => {
    const shuffled = [...players].sort(() => Math.random() - 0.5);
    setRounds(generateRoundRobin(shuffled));
  };

  return (
    <div className="p-4 space-y-4">
      <h1 className="text-xl font-bold">Chess Round Robin Scheduler</h1>
      <div className="flex gap-2">
        <Input
          placeholder="Enter player name"
          value={nameInput}
          onChange={(e) => setNameInput(e.target.value)}
        />
        <Button onClick={addPlayer}>Add Player</Button>
      </div>
      <div>
        <h2 className="text-lg font-semibold">Players ({players.length}):</h2>
        <ul className="list-disc pl-5">
          {players.map((p) => (
            <li key={p}>{p}</li>
          ))}
        </ul>
      </div>
      {players.length >= 2 && (
        <Button onClick={startTournament}>Start Tournament</Button>
      )}
      {rounds.length > 0 && (
        <div className="space-y-4">
          <h2 className="text-lg font-semibold">Rounds</h2>
          {rounds.map((round, idx) => (
            <Card key={idx}>
              <CardContent className="p-4">
                <h3 className="font-bold mb-2">Round {idx + 1}</h3>
                <ul className="list-disc pl-5">
                  {round.map((match, mIdx) => (
                    <li key={mIdx}>
                      {match.white} (White) vs {match.black} (Black)
                    </li>
                  ))}
                </ul>
              </CardContent>
            </Card>
          ))}
        </div>
      )}
    </div>
  );
}
