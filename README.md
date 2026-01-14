# neo_humble

mkdir -p ~/projects/aic_swarm/ros2_workspaces/ws1
mkdir -p ~/projects/aic_swarm/ros2_workspaces/shared/nginx-conf
touch ~/projects/aic_swarm/ros2_workspaces/shared/nginx-conf/doc.conf


docker compose up -d

docker compose down --remove-orphans