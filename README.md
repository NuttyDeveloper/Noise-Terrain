local seed = math.random(-200, 200);
local biomeIncrement = .07;
local heightScale = 10;
local width = 100;
local length = 100;
local partSize = 2;
local bottomColor = Color3.fromRGB(70, 62, 49);
local topColor = Color3.fromRGB(12, 95, 12);

local camera = game.Workspace.CurrentCamera;
camera.CFrame = CFrame.new(Vector3.new(-width * partSize/3, partSize * width/2, -length * partSize/3), Vector3.new());
camera.Focus = CFrame.new();

local partTemplate = Instance.new("Part");
partTemplate.Anchored = true;
partTemplate.CanCollide = false;
partTemplate.TopSurface = Enum.SurfaceType.Smooth;

local function clamp(val, min, max)
	if val < min then
		return min;
	elseif val > max then
		return max;
	end
	return val;
end

local function genTerrain()
	local folder = game.Workspace:FindFirstChild("Folder");
	if folder then
		folder:Destroy();
	end
	folder = Instance.new("Model", game.Workspace);
	folder.Name = "Folder"

	local xOff = 0;
	local yOff = 0;

	for x = 1, width do
		xOff = 0;
		for y = 1, length do
			local noiseValue = clamp(math.noise(xOff, yOff, seed);
				local part = partTemplate:Clone();
				part.Parent = folder;
				part.CFrame = CFrame.new(x*partSize, (noiseValue * heightScale) - heightScale/2, y * partSize);
				part.Name = noiseValue;
				part.Color = bottomColor:Lerp(topColor, noiseValue + .5);
				part.Size = Vector3.new(partSize, heightScale, partSize);

				yOff = yOff + biomeIncrement;
		end
		xOff = xOff + biomeIncrement;
	end
end

genTerrain();
