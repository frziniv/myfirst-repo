# game_agent.py
import time
import random

class GameAgent:
    """
    A class to represent a game agent.
    The agent's primary directive is to achieve the #1 rank.
    """
    def __init__(self, agent_name="Agent_007"):
        self.agent_name = agent_name
        self.goal = "Achieve Rank #1 in all battles."
        self.is_connected = False
        print(f"🚀 Initializing {self.agent_name}. Primary Goal: {self.goal}")

    def connect_to_game_server(self, server_address="127.0.0.1:8080"):
        """Simulates connecting to a game server."""
        print(f"Connecting to game server at {server_address}...")
        time.sleep(1) # Simulate network delay
        self.is_connected = True
        print("✅ Connection successful. Agent is online.")
        
        print("\nAnalyzing game state...")
        time.sleep(0.5)
        # In a real scenario, this would involve processing game data.
        game_data = {
            'player_health': random.randint(50, 100),
            'enemies_nearby': random.randint(0, 5),
            'current_rank': random.randint(2, 50)
        }
        print(f"Analysis complete: Health={game_data['player_health']}, Enemies={game_data['enemies_nearby']}, Rank={game_data['current_rank']}")
        return game_data

    def make_decision(self, game_state):
        """Makes a decision based on the game state."""
        if game_state is None:
            print("No game state to analyze. Standing by.")
            return

        print("Making a strategic decision...")
        time.sleep(1)
        if game_state['enemies_nearby'] > 2:
            print("Decision: High threat detected. Finding a defensive position. 🛡️")
        elif game_state['player_health'] < 60:
            print("Decision: Low health. Searching for health packs. ➕")
        else:
            print("Decision: All clear. Advancing to a strategic location to improve rank. ⚔️")
            
    def run_simulation(self):
        """Runs the main loop of the agent."""
        self.connect_to_game_server()
        try:
            game_round = 1
            while True:
                print(f"\n--- Game Round {game_round} ---")
                state = self.analyze_game_state()
                self.make_decision(state)
                game_round += 1
                time.sleep(3) # Wait before starting the next round
        except KeyboardInterrupt:
            self.disconnect()

    def disconnect(self):
        """Disconnects the agent from the server."""
        print("\n🛑 Disconnecting from server... Mission paused.")
        self.is_connected = False


if __name__ == "__main__":
    # Create an instance of our agent
    my_agent = GameAgent(agent_name="VictorySeeker-AI")
    
    # Run the main agent loop
    my_agent.run_simulation()
